# 자바스크립트 this란?

 this는 일반적으로 메소드를 호출한 객체가 저장되어 있는 속성입니다.



**`this`의 값은 함수를 호출하는 방법**에 의해 결정된다. 



실행환경?

실행가능한 코드가 실행되기위해 필요한 환경

- Variable Environment
  - environment record
  - thisbinding
    - this의 값이 여기서 결정됨
      - 글로벌 실행컨텍스트에서 this는 global object
  - outer environment reference
- Lexical Environment



함수를 누가 호출하냐에서 따라 달라짐

- 전역공간
- 함수 호출
- 메소드 호출
- 콜백 호출
- 생성자 함수 호출



메서드와 함수차이

둘다 어떠한기능을 수행하는것 하지만 메서드는 클래스와 객체에 연관되어있는 함수라는것

클래스내에 선언되있는 함수가 메서드

그외에 그냥 독립적으로 존재하는 것이 함수

함수가 더큰개념으로 보면 된다.

메서드는 a.add() 이런식 함수는 add()



생성자 함수란

생성자는 일단 new를 뜻함

다른언어는 클래스를 이용해서 프로퍼티가 똑같은 객체를 만들어 낼수있는데

자바스크립트는 클래스가 없음! 그래서 생성자 함수를 통해서 객체를 생성함

그외에 객체 리터럴 , Object 생성자 함수 의 방법도 존재한다.



```javascript
// 객체 리터럴
var obj = {
  name : 'BKJang',
  job : 'Developer'
}


// Object 생성자 함수
var obj = new Object();
obj.name = 'BKJang';
obj.job = 'Developer';


// 생성자 함수
function Person(name, job) {
  this.name = name;
  this.job = job;
}

var obj = new Person('BKJang', 'Developer');
```



### 전역공간

브라우저에서는 윈도우 

노드js 에선 global

```javascript
// 브라우저
console.log(this) // window

// 노드
console.log(this) // global
```



### 함수 호출시

브라우저에서는 윈도우 

노드js 에선 global

Arrow Function 에서는 상위컨텍스트의 this



### 메소드 호출시

메소드 호출 주체

```javascript
var a = {
  b: function() {
    console.log(this);
  }
}

a.b(); // this -> a
```



### callback 호출 시

callback 호출 시 `this` 는 기본적으로 함수내부에서와 동일하다.

```jsx
let callback = function() {
  console.log(this);
}

let obj = {
  a: 1,
  b: function(cb) {
    cb();
  }
}

obj.b(callback);
```

아래 코드에서의 `this` 는 무엇일까?

```jsx
let callback = function() {
  console.log(this);
}

let obj = {
  a: 1,
  b: function(cb) {
    cb.call(this);
  }
}

obj.b(callback);
```

### 생성자함수 호출 시

new 키워드를 통해 생성자함수 호출 시 `this` 는 인스턴스를 가리킨다.

즉, 생성자함수 호출 시 객체가 만들어지고, 객체가 this가 되는 것이다.

```jsx
function Who(name, age) {
  this.name = name;
  this.age = age;
}

let jihoon = new Who('hoo00nn', '26ㅠㅠ');

console.log(jihoon);
/*

Who {
  name: 'hoo00nn',
   age: '26ㅠㅠ'
}

*/
```

















