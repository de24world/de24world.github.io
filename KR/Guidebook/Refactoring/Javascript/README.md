
[리팩토링(Refactoring)] 
======================

# 목차
  1. [소개(Introduction)](#소개introduction)
  2. [변수(Variables)](#변수variables)
  3. [함수(Functions)](#함수functions)
  4. [객체와 자료구조(Objects and Data Structures)](#객체와-자료구조objects-and-data-structures)
  5. [클래스(Classes)](#클래스classes)
  6. [SOLID](#SOLID)
  7. [테스트(Testing)](#테스트testing)
  8. [동시성(Concurrency)](#동시성concurrency)
  9. [에러 처리(Error Handling)](#에러-처리error-handling)
 10. [포맷팅(Formatting)](#포맷팅formatting)
 11. [주석(Comments)](#주석comments)
 12. [번역(Translation)](#번역translation)


 ## 소개(Introduction)
Code Review 시 어떻게, 리뷰할 것인가? 재사용이 가능하도록 보다 간견할 코드를 어떻게 작성해볼지 알아보자.


## **조건문(If/Else)**

1. 조건이 여러개일 경우, 조건들을 배열에 넣고, 배열의 includes 메소드를 사용하면 보다 깔끔한 코드를 작성할 수 있습니다.

    **안좋은 예:**
    ```javascript
    if(fruit == 'apple' ||
    fruit == 'watermelon' ||
    fruit == 'cherry' ||
    fruit == 'strawberry' ||
    fruit == 'tomato'
    ) {
    ....
    }
    ```

    **좋은 예:**
    ```javascript
    function test(fruit) {
        const redFruits = ['apple', 'watermelon', 'strawberry']
        if(redFruits.includes(fruit)) {
            console.log('red')
        }
    }
    ```   

 2. 조건문 중첩을 피하고 빨리 리턴하자.

    **안좋은 예:**
    ```javascript
    
    function test(fruit, quantity) {
        const redFruits = ['apple', 'watermelon', 'strawberry']
    
        if(fruit) {
            if(redFruits.includes(fruit)) {
                console.log('red');
                if(quantity > 10) {
                    console.log('big quantity');
                }
            }
        } else {
            throw new Error('No fruit!');
        }
    }
    ```

    **좋은 예:**
    ```javascript
    function test(fruit, quantity) {
        const redFruits = ['apple', 'watermelon', 'strawberry']
        if(!fruit) throw new Error('No fruit!');
        if(!redFruits.includes(fruit)) return;

        console.log('red');
        if(quantity > 10) {
            console.log('big quantity');
        }
    }
    ```

# 1. 조건문 개선 - 중첩된 조건문 처리하기
* Bubble Style => Gateway Style

----
## ○ 참조 문서 및 사이트
* [조건문 개선 - 중첩된 조건문 처리하기(자바)](https://eblo.tistory.com/7)
* [Javscript If/Else 잘 사용하기](https://medium.com/sjk5766/javscript-if-else-%EC%9E%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-386e78524502)

