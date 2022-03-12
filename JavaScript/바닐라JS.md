

오늘 프로그래머스에서 바닐라 자바스크립트로 시험을 쳤다.

아직 바닐라JS는 익숙치않았다.



### fetch

API를 호출하기 위해서는 fetch를 사용하면된다.

```js
fetch(url, options)
  .then(response => response.json())
  .catch((error) => console.log("error:", error));
```

데이터를 받아서 json화시켜서 사용하면된다.



모던자바스크립트의 방식

```js
let response = await fetch(url);

if (response.ok) { // HTTP 상태 코드가 200~299일 경우
  // 응답 몬문을 받습니다(관련 메서드는 아래에서 설명).
  let json = await response.json();
} else {
  alert("HTTP-Error: " + response.status);
}
```



### in , includes

자바스크립트에서 `in`은 파이썬과 다르게 작동한다.

리스트의 인덱스를 인식한다는 점

```js
// 배열
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
0 in trees         // true를 반환합니다.
3 in trees         // true를 반환합니다.
(1 + 2) in trees   // true를 반환합니다. 연산자 우선 순위에 의하여 이 구문의 괄호는 없어도 됩니다.
6 in trees         // false를 반환합니다.
"bay" in trees     // false를 반환합니다. 당신은 배열의 내용이 아닌, 인덱스 값을 명시하여야 합니다.
"length" in trees  // true를 반환합니다. length는 Array(배열) 객체의 속성입니다.

// 미리 정의된 객체
"PI" in Math       // true를 반환합니다.
"P" + "I" in Math  // true를 반환합니다.

// 사용자가 정의한 객체
var myCar = {company: "Lamborghini", model: "Lamborghini Veneno Roadster", year: 2014};
"company" in myCar // true를 반환합니다.
"model" in myCar   // true를 반환합니다.
```

리스트의 요소를 파악하기 위해서는 `includes`를 사용하자

```js
let selectedLanguages= ['css'];
selectedLanguages.includes('css'); //true
```



### remove()

돔요소를 삭제를 할때는 `remove()`를 사용하고 

리스트에서의 요소를 삭제할때는 다르다.

`splice`를 사용하자

```js
let a = [1, 2, 3, 4] 
const idx = a.indexOf(3) 
if (idx > -1) a.splice(idx, 1)
```



다른방법은 `filter`가 있다.

```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```







-------

- 참조
  - https://www.daleseo.com/js-window-fetch/
  - https://ko.javascript.info/fetch
  - https://dgkim5360.tistory.com/entry/deleting-an-item-in-array-javascript
  - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter

