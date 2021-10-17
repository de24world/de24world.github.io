# [CLS] Cumulative Layout Shift

# 1. [CLS] Cumulative Layout Shift란?

- 방문자에게 콘텐츠가 얼마나‌ 불안정한 지 측정하는 사용자 경험 측정 항목 입니다. 현재 보고 있는 페이지에 갑자기 발생하는 레이아웃의 변경은 시각적으로 거슬리며 사용자의 주의를 산만하게 합니다. 즉 사용자가 예상치 못한 레이아웃 이동을 경험하는 빈도를 수량화하므로 시각적 안정성을 측정할 때 중요한 사용자 중심 메트릭입니다. CLS가 낮으면 우수한 사용자 경험을 보장하는 데 도움이 됩니다.

<img src="/KR/Guidebook/CoreWebVitals/CLS/cls_point.png" alt="cls_point" title="cls_point"></img>

## 1.1 CLS 점수

- 일정기간동안 레이아웃 이동이 없는 상태에서 발생하는 예상하지 않은 레이아웃 이동에 대한 누적된 점수이며, 뷰포트에서 이동한 콘텐츠의 양과 영향ㅇㄹ 받은 요사가 이동한 거리를 확인합니다. 좋은 사용자 환경을 제공하려면 사이트에서 CLS점수가 0.1 미만이어야 합니다.
- [구글 Insight](https://developers.google.com/speed/pagespeed/insights) 홈페이지에서 URL 을 입력해서 사이트 분석할 수 있으며, 혹은 localhost는 구글 개발자도구 Lighthouse에서 점수를 확인 가능하다.

<img src="/KR/Guidebook/CoreWebVitals/CLS/cls_point.png" alt="cls_point" title="cls_point"></img>

[CLS점수 계산법 참조 블로그](https://nicj.net/cumulative-layout-shift-in-practice/)

# 2. 레이아웃 이동이 발생하는 원인

- 넓이, 높이가 없는 이미지
- 크기가 없는 광고, 삽입 및 iframe
- 동적으로 삽입된 콘텐츠
- FOIT / FOUT 을 유발하는 웹 글꼴
- DOM을 업데이트하기 전에 네트워크 응답을 기다리는 작업

---

## 2.1 치수(높이, 넓이)가 없는 이미지

- 이미지 및 비디오 요소에 `width`와 `height` 속성을 항상 포함하거나 또는 CSS를 사용하여 필요한 공간(`aspect-radio-box`)를 잡습니다. 이 방법을 사용하면 이미지가 로드되는 동안 브라우저가 문서의 공간을 올바르게 할당할 수 있습니다.

<img src="/KR/Guidebook/CoreWebVitals/CLS/img_width_height.gif" alt="img_width_height" title="img_width_height"></img>

웹 초기(현재도 실무에 많이 사용하지만)에는 브라우저가 이미지를 가져오기 전에 충분한 공간이 할당되었는지 확인하기 위해 `<img>` 태그에 `width`와 `height` 속성을 추가했습니다. 이렇게 하면 `reflow`과 `re-layout`을 최소화할 수 있습니다.

```html
<img src="puppy.jpg" width="640" height="360" alt="Puppy with balloons" />
```

반응형 웹 디자인이 도입된 이후에는 개발자들이 `width`, `height`를 생략하고 대신 CSS를 사용하여 이미지 크기를 조정하기 시작했습니다.

```css
img {
  width: 100%; /* or max-width: 100%; */
  height: auto;
}
```

이 접근 방식의 단점은, 다운로드가 시작되고 브라우저가 크기를 결정할 수 있는 경우에만 이미지를 위한 공간을 할당할 수 있다는 점입니다. 이미지가 로드되면 각 이미지가 화면에 나타나면 reflow 되어 텍스트가 갑자기 화면 아래로 튀어 나가는 것이 일반적이 되었습니다(위의 이미지 참조). 이것은 좋지 않은 사용자 경험을 유발합니다.

이것을 방지하기 위해 영역을 미리 확보를 해두게 되는데, 이 때 사용되는 것이 `aspect-ratio` 입니다.
이미 실무에서 태블릿, 모바일 반응형 대응을 위해 많이 사용되고 있는데요.

[치수를 알고 계산을 하는 방식](https://aspectratiocalculator.com/16-9.html) 외에 새로운 방법이 있어 소개드리겠습니다.

### 2.1.1 `aspect-ratio` 속성 사용하기

- 복잡한 계산없이 간단하게 속성으로 aspect-ratio 를 지정하여 레이아웃 이동을 방지할 수 있습니다.
  `aspect-ratio` 는 CSS4에 새롭게 추가된 속성으로 x/y의 비율을 지정하면 해당 비율로 요소를 나타냅니다.

```html
<div class="box1">16:9 box</div>
<div class="box2">4:3 box</div>
<div class="box3">1:1 box</div>
```

```css
.box1 {
  aspect-ratio: 16/9;
}
.box2 {
  aspect-ratio: 4/3;
}
.box3 {
  aspect-ratio: 1/1;
}
```

[결과]
현재 aspect-ratio 속성은 Firefox 81이상 Chromium 에서 사용할 수 있으며 WebKit(Safari)에도 제공될 예정입니다. 예제 확인 시, 크롬에서는 chrome://flags/ 에서 Experimental Web Platform features 를 Enable 상태로 변경 후 확인해주세요.

- HTML: 이미지가 있는 컨테이너

```html
<div class="box_img">
  <div class="label">▼ 16:9</div>
  <img
    src="https://img.insight.co.kr/static/2019/03/22/700/za85ysn7ubgzuo3z441x.jpg"
    width="640"
    height="390"
    alt="qkqhro"
  />
</div>

<div class="box2_img">
  <div class="label">▼ 4:3</div>
  <img
    src="https://img.insight.co.kr/static/2019/03/22/700/za85ysn7ubgzuo3z441x.jpg"
    width="640"
    height="390"
    alt="qkqhro"
  />
</div>

<div class="box3_img">
  <div class="label">▼ 1:1</div>
  <img
    src="https://img.insight.co.kr/static/2019/03/22/700/za85ysn7ubgzuo3z441x.jpg"
    width="640"
    height="390"
    alt="qkqhro"
  />
</div>
```

```css
div[class^="box"] {
  display: inline-block;
  width: 300px;
  margin-bottom: 40px;
  padding: 10px 20px;
  vertical-align: top;
}

/* 이미지 속성에 height: auto; 를 설정하여
이미지 높이가 고정된 값(inline으로 선언한 height값)이 되지 않도록 합니다. */
img {
  width: 100%;
  height: auto;
}

/* 컨테이너에 원하는 aspect-ratio 선언 */
.box1_img img { aspect-ratio: 16/9; }
.box2_img img { aspect-ratio: 4/3; }
.box3_img img { aspect-ratio: 1/1; }
...
```

모든 브라우저의 User [Agent Stylesheet](https://developer.mozilla.org/ko/docs/Web/CSS/Cascade#user-agent_stylesheets) 는 요소의 기존 `width` 및 `height` 속성에 따라 기본 `aspect-ratio` 를 추가할 수도 있습니다.

```css
img {
  aspect-ratio: attr(width) / attr(height);
}
```

이미지가 로드되기 전에 `width` 및 `height` 속성을 기준으로 aspect-ratio 를 계산합니다. 이 정보는 레이아웃 계산을 시작할 때 제공됩니다.
이미지가 특정 `width`(예: `width: 100%`)로 표시되는 즉시 aspect-ratio를 사용하여 높이를 계산합니다.

### 2.1.2 반응형 이미지 처리

img 태그의 `width` 및 `height` 속성을 설정할 수 있도록 각 이미지는 같은 aspect-ratio 를 사용해야 합니다.

또 기존의 img 태그는 오직 하나의 소스 파일만 제시하도록 되어 있는데, `srcset`과 `sizes`라는 두 가지 새로운 속성을 사용해 브라우저가 이미지를 나타내는데에 도움이 되는 몇 가지 추가 소스 이미지와 힌트를 제공 할 수 있습니다.

```html
<img
  width="1000"
  height="1000"
  src="puppy-1000.jpg"
  srcset="puppy-1000.jpg 1000w, puppy-2000.jpg 2000w, puppy-3000.jpg 3000w"
  alt="Puppy with balloons"
/>
```

그리고 하나의 이미지가 좁은 뷰포트에 잘려진 일부 이미지로 보여지게도 할 수 있습니다.

```html
<picture>
  <source media="(max-width: 799px)" srcset="puppy-480w-cropped.jpg" />
  <source media="(min-width: 800px)" srcset="puppy-800w.jpg" />
  <img src="puppy-800w.jpg" alt="Puppy with balloons" />
</picture>
```

이것은 Art direction problem 에 따른 이미지 처리 방법입니다. 자세한 내용은 아래 링크 참고 부탁드립니다.
https://developer.mozilla.org/ko/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images#Art_direction

## 3.2 Jenkins Plugin

- 젠킨스의 장점 중 하나는 다양한 플러그인으로 기능을 확장 할 수 있다.
- 예를 들어 git plugin을 설치하면 git과 jenkins를 쉽게 연동할 수 있다.

## 3.3 Jenkins 설정

- Jenkins 접속하여 새로 생성하고 싶으면 왼쪽 메뉴에 **New Item** 을 클릭하여 Freestyle project(혹은 다르게도 가능)을 눌러 새 작업을 생성해준다.
  <img src="/KR/Guidebook/Jenkins/jenkins_configure.png" alt="jenkins_configure" title="jenkins_configure"></img>

## ○ 참고 영상

- [Optimize for Core Web Vitals](https://youtu.be/AQqFZ5t8uNc)
- [ARIA에 대해서 HTML 접근성 향상시키기](https://youtu.be/MQHNTzdqet0)

## ○ 참조 문서 및 사이트

- [새로운 웹페이지 성능 측정 지표 CLS(Cumulative Layout Shift)](https://wit.nts-corp.com/2020/12/28/6240)
- [Cumulative Layout Shift(누적 레이아웃 이동, CLS)](https://web.dev/i18n/ko/cls/)
- [클린코드란 무엇인가?](https://www.samsungsds.com/kr/story/cleancode-0823.html)
