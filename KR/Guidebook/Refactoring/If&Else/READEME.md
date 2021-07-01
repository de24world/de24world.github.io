
[리팩토링(Refactoring) - If/Else] 
======================


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

 3. 함수의 Default parameter, 객체 Destructuring 사용하기
    - Javascript 함수 매개변수가 null, undefined를 체크하는 경우가 있는데, 이때 `default parameter` 를 사용한다.   
        **안좋은 예:**
        ```javascript
        function test(fruit, quantity) {
            if(!fruit) return;
            const q = quantity || 1; 

            console.log(`We have ${q} ${fruit}!`);
        }
        ```

        **좋은 예:**
        ```javascript
        function test(fruit, quantity = 1) { 
            if(!fruit) return;
            console.log(`We have ${quantity} ${fruit}!`);
        }
        ```   
   
    - 매개변수가 객체일 경우   
        **안좋은 예:**
        ```javascript
        function test(fruit) { 
            if(fruit && fruit.name)  {
                console.log (fruit.name);
            } else {
                console.log('unknown');
            }
        }
        ```

        **좋은 예:**
        ```javascript
        function test({name} = {}) {
            console.log (name || 'unknown');
        }
        ```   

 4. switch 보단 Map/객체 literal을 사용하자

    **안좋은 예:**
    ```javascript
    function test(color) {
        switch (color) {
            case 'red':
                return ['apple', 'strawberry'];
            case 'yellow':
                return ['banana', 'pineapple'];
            case 'purple':
                return ['grape', 'plum'];
            default:
                return [];
        }
    }
    ```

    **좋은 예:객체 리터럴(Object literal)**
    ```javascript
    const fruitColor = {
        red: ['apple', 'strawberry'],
        yellow: ['banana', 'pineapple'],
        purple: ['grape', 'plum']
    };

    function test(color) {
        return fruitColor[color] || [];
    }
    ```

    **좋은 예:Map**
    ```javascript
    const fruitColor = new Map()
        .set('red', ['apple', 'strawberry'])
        .set('yellow', ['banana', 'pineapple'])
        .set('purple', ['grape', 'plum']);

    function test(color) {
        return fruitColor.get(color) || [];
    }
    ```


5. 삼항 연산자(Ternary Operators)

    **안좋은 예:**
    ```javascript
    let drink = 'coffee';
    if(isNight) {
        drink = 'soju'
    }
    ```

    **좋은 예:**
    ```javascript
    const drink = isNight? 'soju' : 'coffee'
    ```   

6. &&, || (short circuit 사용하기)

    **좋은 예:**
    ```javascript
    const drink = isNight && 'soju' || 'coffee'
    ```   

    **좋은 예:조건이 객체와 객체의 속성을 체크할 경우**
    ```javascript
    let message = null
    if (user && user.name) {
        message = `Welcome, ${user.name}!`
    }
    ```   

----
## ○ 참조 문서 및 사이트
* [Javscript If/Else 잘 사용하기](https://medium.com/sjk5766/javscript-if-else-%EC%9E%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-386e78524502)

