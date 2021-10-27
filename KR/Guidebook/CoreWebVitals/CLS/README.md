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

참고로 <U>대부분 문제가 img 의 높이와 넓이가 없어서 layout 밀리는 경우가 많다. 예를 들어, 어떤 button이나 <p> 태그가 밀리는 경우 주위에 `height`, `width`가 없는 `<img>` 태그가 있는지 꼭 확인해준다. 해당 이미지가 없어서 다른 요소가 layout 밀리는 경우가 많기 때문이다. </U>

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

<img src="/KR/Guidebook/CoreWebVitals/CLS/srcet_size.jpeg" alt="srcet_size" title="srcet_size"></img>

이것은 Art direction problem 에 따른 이미지 처리 방법입니다. 자세한 내용은 아래 링크 참고 부탁드립니다.
https://developer.mozilla.org/ko/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images#Art_direction

### 2.1.3 img 파일 대신 svg 파일을 활용하자

- 개인적으로 프로젝트 진행하면서 느낀점은 img 파일 대신 svg 파일을 활용하는 것도 좋은 방법이라고 생각한다. svg파일로 된 이미지가 많으면 img 파일을 대체하자. 개인적으로 React 프로젝트 진행시 svgr 이라는 라이브러리를 사용해서 img 파일을 대체했더니 번거로움을 훨씬 줄어들었다. 왜냐하면 svg 파일에는 대부분 이미 width와 height 값이 포함되어있기 때문이다.

## 2. 크기가 정의되지 않은 광고, Embed 및 Ifrme

## 2.1 광고

광고느 ㄴ웹에서 레이아웃 이동에 가장 큰 영향을 주는 요소 중 하나입니다. 광고 크기는 높은 클릭율과 성능,수익에 관련이 있기 때문에 광고 게시자는 종종 동적인 광고 크기를 지원합니다. 이러한 동적인 광고 크기는 현재 보고 있는 콘텐츠를 페이지 아래로 밀어버릴 수 있어 사용자 환경이 최적화되지 않을 수 있습니다.

광고의 life-cycle 동안 많은 지점에서 레이아웃 이동이 발생할 수 있습니다.

- 사이트가 DOM에 광고 컨테이너를 삽입할 때
- 사이트에서 자사 코드를 사용하여 광고 컨테이너의 크기를 조정할 때
- 광고 태그 라이브러리가 로드될 때(광고 컨테이너의 크기가 조정될 때)
- 광고가 컨테이너를 채울 때(최종 광고의 크기가 다른 경우 크기가 조정됨)

다음과 같은 방법으로 레이아웃 변화를 줄일 수 있습니다.

- 광고 슬롯을 위한 공간을 정적으로 확보합니다. 즉, 광고 태그 라이브러리가 로드되기 전에 요소의 스타일을 지정합니다. 슬롯의 크기를 지정하여 (위의 img tag 참조) 레이아웃 이동을 방지하세요.
- 뷰포트 상단 근처에 고정되지 않은 광고를 배치할 때 주의하세요. 아래 예시처럼 광고를 월드 비전 로고 아래로 이동하고슬롯을 위한 충분한 공간을 확보하는 것이 좋습니다.
- placeholder 를 표시하여 광고 슬롯이 표시될 때, 반환된 광고가 없는 경우 확보된 공간을 축소하지 마십시오.
- 광고 슬롯에 가능한 가장 큰 크기를 확보하여 레이아웃 이동을 방지하십시오. 더 작은 광고 소재가 슬롯을 채우면 빈 공간이 생길 위험이 있습니다.
- 이전 데이터를 기반으로 광고 슬롯에 가장 적합한 크기를 선택합니다.

<img src="/KR/Guidebook/CoreWebVitals/CLS/advertising_slot.gif" alt="advertising_slot" title="advertising_slot"></img>

### 2.1.1 광고 슬롯을 위한 정적 공간 확보

최대한 작은 사이즈의 광고 서비스를 사용 하기를 권장합니다. 만약 광고 슬롯을 사용하게 된다면, 정적으로 스타일하기를 추천하며 그렇지 않으면 페이지 레이아웃 로드 후에 광고 슬롯 요소의 크기가 변경될 수 있습니다.

### 2.1.2 뷰포트 상단 근처에 광고 배치하지 않기

뷰포트 상단 근처에 있는 광고는 가운데이 있는 광고보다 더 큰 레이아웃 이동을 유발할 수 있습니다. 왜냐하면 상단의 광고는 아래의 콘텐츠를 변화를 일으키는 더 많은 요소가 포함되어있기 때문이다. 반대로 뷰포트의 중간간 근처에 있는 광고는 위의 콘텐츠 이동할 가능성이 비교적 적습니다.

## 2.2 [Embeds and iframes](https://web.dev/optimize-cls/#embeds-and-iframes)

Embed 가능한 위젯을 사용하면 페이지에 삽입 가능한 웹 콘텐츠(예 : YouTube의 비디오, Google Maps의 지도, 소셜 미디어 게시물 등)를 포함할 수 있습니다. 이러한 Embeds는 다음과 같은 형식을 가지고 있습니다.

- HTML fallback 및 fallback을 embed로 변환하는 JavaScript 태그
- inline HTML snippet
- iframe 삽입

이러한 Embeds는 Embed 크기 및 규모가 얼마나 될 것인지 미리 알기 어렵습니다. 만

-예: 소셜 미디어 포스트의 경우 embed 이미지, 비디오, 여러 줄의 텍스트 등이 있는지

따라서 Embeds를 제공하는 플랫폼은 Embeds를 위한 항상 충분한 공간을 확보하지는 않으며, 최종적으로 로드할 때 레이아웃 이동이 발생할 수 있습니다.

## 4. FOIT / FOUT 를 유발하는 웹 글꼴

웹 글꼴을 다운로드하고 렌더링하면 다음 두 가지 방식때문에 레이아웃이 변경될 수 있습니다. 만

- FOIT(Flash Of Invisible Text) : 웹 폰트가 적용되지 않은 텍스트가 보이지 않는 상태(insvisible)에서 폰트가 바뀌면서 텍스트 번쩍이 일어남
- FOUT(Flash Of Unstyled Text) : 웹 폰트가 적용되지 않은 Fallback 폰트 상태(unstyled)에서 폰트가 바뀌면서 텍스트 번쩍이 일어남

<img src="/KR/Guidebook/CoreWebVitals/CLS/FOIT_FOUT.gif" alt="FOIT_FOUT" title="FOIT_FOUT"></img>

다음 도구를 사용하면 이를 최소화할 수 있습니다.
`font-display`를 사용하면 `auto`, `swap`, `block`, `fallback`, `optional` 등의 값을 사용하여 사용자 정의 폰트의 렌더링 동작을 수정할 수 있습니다. 그러나 위의 방법으로는 (`optional` 제외) 모두 re-layout 될 수 있습니다.

Chrome 83부터 다음도 권장할 수 있습니다.

- 주요 웹 글꼴에 `<link el=preload>`를 사용하면 사전 로드된 폰트가 첫 번째 paint와 일치할 가능성이 커지며, 이 경우 레이아웃 이동이 없습니다.
- `<link el=preload>`와 `font-display: optional`을 조합하여 사용할 수 있습니다.
  자세한 내용은 [Prevent layout shifting and flashes of invisible text (FOIT) by preloading optional fonts](https://web.dev/preload-optional-fonts/) 를 참고해주세요.

## ○ 참고 영상

- [Optimize for Core Web Vitals](https://youtu.be/AQqFZ5t8uNc)
- [ARIA에 대해서 HTML 접근성 향상시키기](https://youtu.be/MQHNTzdqet0)

## ○ 참조 문서 및 사이트

- [새로운 웹페이지 성능 측정 지표 CLS(Cumulative Layout Shift)](https://wit.nts-corp.com/2020/12/28/6240)
- [Cumulative Layout Shift(누적 레이아웃 이동, CLS)](https://web.dev/i18n/ko/cls/)
- [웹 폰트 사용과 최적화의 최근 동향](https://d2.naver.com/helloworld/4969726)
