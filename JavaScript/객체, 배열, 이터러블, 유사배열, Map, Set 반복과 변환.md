# 객체, 배열, 이터러블, 유사배열, Map, Set

> 현재 자바스크립트에서는 다양한 문법을 제시한다. 그 중 헷갈리는게 배열, 이터러블 같은 것들을 나열하는 문법 들이 많아서 정리하려고 한다.



### 객체

- `for ... in` : 객체의 모든 키를 순환합니다.
  - 프로퍼티는 시간순으로 정렬되서 나타납니다.
    - 정수프로퍼티는 예외
  - 심볼은 '심볼형 프로퍼티 숨기기(hiding symbolic property)' 라는 원칙에 의해 배제됩니다.

### 문자열

- `for ... of` : 한 문자씩 순환합니다.

### 배열 

- `for`
- `for ... of`

- `forEach` : 배열 요소마다 함수 적용이가능합니다.

  -  ```js
     ["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
       alert(`${item} is at index ${index} in ${array}`);
     });
     ```

- `map`

  - `map`은 배열 요소 전체를 대상으로 함수를 적용하고 배열로 반환합니다.

  - ```js
    let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
    alert(lengths); // 5,7,6
    ```

- `filter`

  - ```js
    const map_reuslt = [1, 2, 3, 4].map((value, index, array)=>{ console.log(value); // 1, 2, 3, 4 출력 return value*10; // 각 요소에 10을 곱한 값을 배열로 반환 }) console.log(map_reuslt); // [ 10, 20, 30, 40 ]
    ```

- `reduce`

  - 배열 내 요소에 대해 중복으로 함수를 적용할 수 있습니다.

  - ```js
    let value = arr.reduce(function(accumulator, item, index, array) {
      // ...
    }, [initial]);
    ```

    - `accumulator` – 이전 함수 호출의 결과. `initial`은 함수 최초 호출 시 사용되는 초깃값을 나타냄(옵션)
    - `item` – 현재 배열 요소
    - `index` – 요소의 위치
    - `array` – 배열

- **`for ... in` 은 객체를 위한것이다! 쓰지말자!!**

### iterable 객체

- `iterable`은 메서드`Symbol.iterator`가 구현되어있습니다.
  - 종류는 `String`, `Array`, `Map`, `Set`, `DOM컬렉션`
- `for ... of` 사용이 가능합니다.
  - 문자열은 `iterable` 합니다.

### 유사배열

- `유사배열`은 `length`프로퍼티가 있어 배열처럼 보이는 `객체`입니다.

### Map

- 객체와 유사하지만 `key`에 다양한 자료형을 넣을 수 있습니다.
- 맵의 프로퍼티의 삽입 순서를 기억합니다.
- `forEach` : 배열처럼 지원합니다.
- `for ... of`
- `map.keys()` : 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환합니다.
- `map.values()`: 각 요소의 값을 모은 이터러블 객체를 반환합니다.
- `map.entries()`: 요소의 `[키, 값]`을 한 쌍으로 하는 이터러블 객체를 반환합니다. 이 `iterable` 객체는 `for...of`반복문의 기초로 쓰입니다.

### Set

- `forEach`

- `for ... of`

  - ```js
    let set = new Set(["oranges", "apples", "bananas"]);
    for (let value of set) alert(value);
    
    set.forEach((value, valueAgain, set) => {
      alert(value);
    });
    ```

- `set.keys()` – 셋 내의 모든 값을 포함하는 `iterable` 객체를 반환합니다.

- `set.values()` – `set.keys`와 동일한 작업을 합니다. `맵`과의 호환성을 위해 만들어진 메서드입니다.

- `set.entries()` – 셋 내의 각 값을 이용해 만든 `[value, value]` 배열을 포함하는 `iterable` 객체를 반환합니다. `맵`과의 호환성을 위해 만들어졌습니다.

### 일반 객체 순회 전용 메서드

- ```js
  let user = {
    name: "John",
    age: 30
  };
  ```

- `Object.keys(user) = ["name", "age"]`

- `Object.values(user) = ["John", 30]`

- `Object.entries(user) = [ ["name","John"], ["age",30] ]`

- 이들은 `iterable`이 아닌 `배열`로 반환해줍니다. 





-----------



## 변환

> 각 자료구조들 마다 서로 변환하는 방법을 갖고 있습니다.
>
> 작정하고 하면 방법은 무궁무진하지만 어느정도 내부메서드로 잡혀있는 것들로 정리했습니다.



- 배열 :arrow_right:  문자열
  - `toString`

- 유사 배열 :arrow_right:  이터러블 :arrow_right:  유사배열
  - 유사 배열이 되기 위해서 `length` 프로퍼티가 필요합니다.
  - 이터러블 객체가 되기 위해서는 메서드`Symbol.iterator`가 필요합니다.

- 이터러블:arrow_right: 배열

  - `Array.from(obj[,mapFn,thisArg])`

  - ```js
    // 각 숫자를 제곱
    let arr = Array.from(range, num => num * num);
    alert(arr); // 1,4,9,16,25
    ```

- 객체 :arrow_right: 맵

  - `Object.entries(obj)`

  - ```js
    let obj = {
      name: "John",
      age: 30
    };
    let map = new Map(Object.entries(obj));
    alert( map.get('name') ); // John
    ```

- 맵 :arrow_right: 객체

  - `Object.fromEntries(map.entries())`

- 객체 :arrow_right: 셋
  - `set.entries(obj)`
    - 셋 내의 각 값을 이용해 만든 `[value, value]` 배열을 포함하는 이터러블 객체를 반환합니다. `맵`과의 호환성을 위해 만들어졌습니다.

- 셋 :arrow_right: 객체

  - `Array.from(obj[,mapFn,thisArg])` 을 통해서 요소를 맵핑해서 직접 만들어 줄수 있습니다.

  - ```js
    const uom = new Set(['inches', 'centimeters', 'yards', 'meters']);
    const res = Object.assign(...Array.from(uom, v => ({[v]:''})));
    console.log(res);
    ```

    



-------

### 참조

https://curryyou.tistory.com/202

https://ko.javascript.info



