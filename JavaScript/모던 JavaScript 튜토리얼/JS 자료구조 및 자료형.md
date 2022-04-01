## 원시값의 메서드

- 원시값에서도 객체처럼 메서드를 호출할수있습니다.

  1. 원시값은 원시값 그대로 남겨둬 단일 값 형태를 유지합니다.
  2. 문자열, 숫자, 불린, 심볼의 메서드와 프로퍼티에 접근할 수 있도록 언어 차원에서 허용합니다.
  3. 이를 가능하게 하기 위해, 원시값이 메서드나 프로퍼티에 접근하려 하면 추가 기능을 제공해주는 특수한 객체, "원시 래퍼 객체(object wrapper)"를 만들어 줍니다. 이 객체는 곧 삭제됩니다.

- 각 레퍼객체는 원시자료형 이름 그대로 부릅니다.

- ```js
  let str = "Hello";
  
  alert( str.toUpperCase() ); // HELLO
  ```

  - 문자열 `str`은 원시값이므로 원시값의 프로퍼티(toUpperCase)에 접근하는 순간 특별한 객체가 만들어집니다. 이 객체는 문자열의 값을 알고 있고, `toUpperCase()`와 같은 유용한 메서드를 가지고 있습니다.
  - 메서드가 실행되고, 새로운 문자열이 반환됩니다(`alert` 창에 이 문자열이 출력됩니다).
  - 특별한 객체는 파괴되고, 원시값 `str`만 남습니다.

- null 과 undefined의 메서드는 없습니다.



## 숫자형

- e는 오른쪽수에 있는 만큼 10의 거듭제곱을 곱합니다.

  - `1e3 = 1000`, `2e-6= 0.000002`

- `0x` 는 16진수 `0o`는 8진수 `0b`는 2진수

- `num.toString(base)` base로 진법을 바꾼후 문자열로 변환해서 반환합니다.

  - base는 2~ 36까지 가능
  - 숫자를 직접쓰고 싶으면 `.`을 추가해서 소수가 없다는 걸 표현해야합니다.
    - `1234..toString(16)`
    - `(1234).toString(16)`  괄호도 사용가능

- `Math.floor` : 버림, `Math.ceil`: 올림, `Math.round`: 반올림, `Math.trunc`: 소수부 무시 

- 일정 소숫점을 남기고 싶을 경우

  - 원하는 만큼 10을 곱하고 버림하고 다시 나누기
  - `toFixed(n)` 사용하기 근데 이거는 문자형으로 반환됨으로 `+`를 붙여주는 식으로 사용된다.
    - 이거는 반올림으로 적용됨

- `0.1+0.2 = 0.3000000000004` 이런식으로 나타남 왜냐면 2진법으로 나타내기 힘듬 이를 정밀도 손실이라고함

  - 해결방법은 `toFixed(n)`임

- `NaN`인지 확인하기위한 `isNaN(value)` , 문자열이 숫자인지 확인하기위한 `isFinite(value)`

- `is`는 비교결과가 정확해야하는 경우 사용되면 `===`보다 정확합니다.

  - `Object.is(NaN, NaN) === true`임.
  - `0`과 `-0`이 다르게 취급되어야 할 때: `Object.is(0, -0) === false`

- `parseInt`, `parseFloat`는 시작부터 숫자를 읽어서 반환해 줌

  - ```js
    alert( parseInt('100px') ); // 100
    alert( parseFloat('12.5em') ); // 12.5
    alert( parseInt('a123') ); // NaN,
    ```

  - 두번째 인수를 설정할 수 있는데 이는 `진수`를 설정해줍니다.

    - `parseInt('0xff', 16) ); // 255`
    - parseInt('ff', 16) ); // 255

- `Math.random()`: 0과 1사이의 난수를 반환합니다.

- `Math.max`, `Math.min`  인수 중 최대/최솟값 반환

- `Math.pow(n, power)` n을 power 제곱한 값을 나타넵



## 문자열

- 백틱을 사용하면 표현식을 중간에 넣을수 있는데 이거를 `템플릿 리터럴`이라고한다.

  - 여러줄도 가능

    - 따옴표는 불가능함

  - `템플릿 함수`에도 쓰이는데 

    - ```js
      func `string` //이케하면 func함수가 백틱안에있는 결과를 인수로 받는다.
      //이런걸 태그드 템플릿이라고 한다.
      ```

    - 이거 쓰면 사용자 지정 템플릿에 맞는 문자열 생성가능 그런데 자주 쓰이진 않는다고함

    - 템플릿 

- `length`는 숫자가 저장되는 프로퍼티이다.

- 특정위치의 글자를 접근하는데에는 `[pos]` 와 `str.charAt(pos)`를 쓴다.

  - 대부분 대괄호 사용합니다.
  - 글자가 없으면 `[]`는 `undefined` `charAt`은 빈문자열 반환
  - `for of`를 통해서 글자를 대상으로 반복작업 가능

- 문자열은 수정이 불가능합니다.

- 대소문자 변경에는 `toLowerCase()`, `toUpperCase()`씁니다.

- 부분 문자열을 찾는데 여러가지 방법이 있습니다.

  - `str.indexOf(substr,pos)` : pos 부터 시작해서 substr을 찾아서 위치를 반환, 못찾으면 -1
    - `str.lastIndexOf(substr,pos)`는 뒤에서 부터 찾음 (pos 부터 범위인건 같음)

    - `if(~str.indexOf("..."))` 를 쓰면 부분문자열인지 확인하는 거임
      - `~`이 붙으면 값이 `~n` 이 `-(n+1)`이 되니깐 -1 출력이 0 출력되서 false가 되는거임
  - `includes`는 참거짓으로  리턴함
    - 위에 것들은 찾을때 `===` 사용함  즉, `false`는 형변환없이 그대로 찾는다는 점
    - 근데 `includes`는 ` NaN`도 잘찾음, 위에는 못함
      - 원래 `NaN`은 `===`에 무조건 `false`임
  - `startsWith`는 특정 문자열로 시작하는지
  - `endsWith`는 특정 문자열로 끝나는지

- 부분문자열 추출

  - `str.slice(start[,end])` : `end`는 포함안함 없으면 끝까지
  - `str.substring(start[,end])`: 이거는 `start`와 `end`의 대소가 상관없음 ( 음수는 0임)
  - `str.substr(start,length)` : 시작부터 개수를 출력
    - 구식
  - `slice`로 대부분 처리가 됨

- 글자비교할때 `str.codePointAt(pos)`쓰면 `pos`에 위치한 글자 코드가 뭔지 알려줌

  - 그반대로는 `String.fromCodePoint(code)`
  - `\u`뒤에 해당되는 코드의 16진수 붙이면 글자 나옴
  - 복잡한 글자들 비교는 `str.localeCompare(str2)` 쓰면 된다.
    - 양수이면 `str`이 큰거
    - 음수이면 `str2`가 큰거

- 대부분의 글자는 2바이트이다. 하지만 이걸로 충분이 나타내지못함 그래서

  - 2바이트 글자를 쌍으로 쓰는 `서로게이트 쌍`을 사용해서 나타낸다.

  - ```js
    // charCodeAt는 서로게이트 쌍을 처리하지 못하기 때문에 서로게이트 쌍을 구성하는 부분에 대한 코드를 반환합니다.
    alert( '𝒳'.charCodeAt(0).toString(16) ); // d835, 0xd800과 0xdbff 사이의 코드
    alert( '𝒳'.charCodeAt(1).toString(16) ); // dcb3, 0xdc00과 0xdfff 사이의 코드
    ```

- 발음 기호는 유니코드 문자를 붙여서 만들수있다.

  - ```js
    alert( 'S\u0307' ); // Ṡ
    alert( 'S\u0307\u0323' ); // Ṩ
    alert( 'S\u0323\u0307' ); // Ṩ
    ```

  - 근데 마지막 두개는 값이 다르게 나온다 그래서 정규화 해줘야된다.

    - ```js
      alert( "S\u0307\u0323".normalize() == "S\u0323\u0307".normalize() ); // true
      //이경우 이미 UTF-16 테이블에 있어서 "\u1e68" 로 값을 가지고 있다.
      ```



## 배열

- 배열의 자료형에는 제약이 없습니다.
- `pop()`: 배열끝 제거하고 반환
- `push()`: 배열끝 요소 추가
- `shift()`: 배열앞 제거하고 반환
- `unshift()`: 배열앞 요소 추가
- 배열은 특별한 종류의 `객체`입니다. 키가 숫자라는 점!!!
  - 객체여서 참조로 인해서 복사가 됨
  - 숫자가 키여서 순서가있는 특별하 메소드 제공
  - `length` 프로퍼티 제공
  - 순서가있는 자료를 저장하는 특수한 자료구조다! 목적에 맞지 않으면 `{}` 쓰자
- 반복하기 위해서는 
  - `for` 
  - `for .. of` : 값만 얻을수있음
  - 객체이기 때문에 `for .. in` 도 됨
    - 객체에 최적화되있어서 모든 프로퍼티 대상으로 순회를 함
    - 배열에는 **쓰지말자**
- 배열의 `length`는 가장큰 인덱스에 1을 더한값이다.
  - 배열 중간에 비어있어도 큰값이 나온다는 것
  - 특이한 점은 쓰기가 가능하다는 점 줄이면 배열이 잘리고 늘리면 아무일 안일어남
- 배열만드는데 `new Array(number)`도 있는데 숫자에 맞춰서 요소가없는 길이는 있는 배열이 생성됨, 잘모르면 `[]`를 쓰자
- 배열에는 `toString`이 구현되어있어서 출력하려면 문자열이 나옵니다.



## 배열과 메서드



- `splice(index[, deleteCount, elem1, ..., elemN])`

  - `index`에 해당되는 위치부터 `deleteCount`만큼의 수를 제거합니다. (제거된 요소는 반환!)

  - 그리고 `elem`을 추가를 합니다.

  - ```js
    let arr = ["I", "study", "JavaScript", "right", "now"];
    // 처음(0) 세 개(3)의 요소를 지우고, 이 자리를 다른 요소로 대체합니다.
    arr.splice(0, 3, "Let's", "dance");
    alert( arr ) // now ["Let's", "dance", "right", "now"]
    ```

  - 음수 인덱스도 사용가능

- `slice([start], [end])`

  - `start` 부터 `end` 직전 까지의 요소들을 복사하여 새로운 배열을 반환합니다.
  - 음수가능
  - `splice`와는 다르게 배열로 반환함 
  - 인수를 안넣어서 그대로 복사본을 만들수 있음

- `concat(arg1, arg2...)`

  - 인수가 합쳐짐
    - 배열이면 배열 요소들이 합쳐지고
    - 객체는 그대로 합쳐짐
      - 근데 `Symbol.isConcatSpreadable`이게 `true` 이면 배열로 취급
      - 객체의 프로퍼티`값` 이 더해짐

- `forEach` 

  - 인수를 통해서 주어진 함수를 배열 요소에 적용 가능

  - ```js
    ["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
      alert(`${item} is at index ${index} in ${array}`);
    });
    ```



-  `find`


  - 배열 내 객체를 찾을 때 사용

  - ```js
    let result = arr.find(function(item, index, array) {
      // true가 반환되면 반복이 멈추고 해당 요소를 반환합니다.
      // 조건에 해당하는 요소가 없으면 undefined를 반환합니다.
        //하나의 요소만 찾음!!!
    });
    ```

  - ```js
    let users = [
      {id: 1, name: "John"},
      {id: 2, name: "Pete"},
      {id: 3, name: "Mary"}
    ];
    let user = users.find(item => item.id == 1);
    alert(user.name); // John
    ```

  - `findindex`는 인덱스를 반환함 조건에 맞는게 없으면 `-1`을 반환한다.

- `filter`


  - `find`는 하나의 요소만 찾는다. 여러개를 찾으려면 `filter`를 사용한다.
  - 배열을 반환한다. 


- `map`

  - 배열 요소 전체를 대상으로 함수를 호출하고 결과를 배열로 반환해줍니다.

  - ```js
    let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
    alert(lengths); // 5,7,6
    ```

- `sort`

  -  배열의 요소를 정리를 하는데 요소안의 값은 문자열로 취급됩니다.

  - `sort`의 인수로 함수를 넣어줘야하며 이 함수는 값두개를 비교해야하며 반환값도 있어야합니다.

  - ```js
    function compare(a, b) {
      if (a > b) return 1; // 첫 번째 값이 두 번째 값보다 큰 경우
      if (a == b) return 0; // 두 값이 같은 경우
      if (a < b) return -1; //  첫 번째 값이 두 번째 값보다 작은 경우
    }
    
    arr.sort( (a, b) => a - b ); // 깔끔
    ```

  - 문자열에서는 `localeCompare`을 사용하면됩니다.

- `reverse`

- `split`을 쓰면 문자열을 배열로 바꿀수 있습니다.

- `join`은 배열을 문자열로 만들어줍니다.

- `reduce`를 이용하면 배열내 요소에 중복으로 함수를 적용할수있습니다.

  - ```js
    let value = arr.reduce(function(accumulator, item, index, array) {
      // ...
    }, [initial]);
    ```

    - `accumulator` – 이전 함수 호출의 결과. `initial`은 함수 최초 호출 시 사용되는 초깃값을 나타냄(옵션)
    - `item` – 현재 배열 요소
    - `index` – 요소의 위치
    - `array` – 배열

  - ```js
    let arr = [1, 2, 3, 4, 5];
    let result = arr.reduce((sum, current) => sum + current, 0);
    alert(result); // 15
    ```

  - 초깃값이 없으면 배열의 첫번째 요소가 되지만 빈배열이라면 에러를 발생하므로 주의를 기울여야합니다.

  - `reduceRight`는 배열의 오른쪽 부터 연산을 수행 합니다.



- 배열도 객체이기 때문에 배열인것을 확인하기 위해서는 `isArray`를 사용합니다.

- 대부분 함수를 호출하는 배열메서드는 `thisArg` 매개변수를 옵션으로 받습니다.

  - ```js
    arr.find(func, thisArg);
    arr.filter(func, thisArg);
    arr.map(func, thisArg);
    // thisArg는 선택적으로 사용할 수 있는 마지막 인수입니다.
    ```

  - thisArg는 func의 this가 됩니다.

  - this를 지정해줄 수 있습니다.



## iterable 객체

- 배열을 일반화한 객체가 반복가능(이터러블)한 객체다.

  - 즉, 이터러블 객체는 언제나 `for of ` 사용이 가능하다.

- ```js
  let range = {
    from: 1,
    to: 5
  };
  ```

  - 이터러블로 만들려면 `Symbol.iterator` 메서드를 추가해야한다.

  - `for of`의 경우 시작시`Symbol.iterator` 를 호출 하기 때문, 없으면 에러를 출력한다.

    - 다음에는 `next()`를 호출한다. `next()`의 반환값은  `{done: Boolean, value: any}`다.
      - `done`이 `true`면 끝났다는 말

  - ```js
    let range = {
      from: 1,
      to: 5
      [Symbol.iterator](){
        current: this.from,
        last: this.to,
    	},
      next() {
            // 4. next()는 값을 객체 {done:.., value :...}형태로 반환해야 합니다.
          if (this.current <= this.last) {
              return { done: false, value: this.current++ };
          } else {
              return { done: true };
          }
      },
    };
    
    // 이제 의도한 대로 동작합니다!
    for (let num of range) {
      alert(num); // 1, then 2, 3, 4, 5
    }
    ```

- 문자열은 이터러블 하다.

- 이터러블은 메서드`Symbol.iterator`가 구현되어있습니다.

  - 유사배열은 인덱스와 `length`프로퍼티가 있어서 배열처럼 보이는 객체입니다.

  - ```js
    // 유사 배열 객체
    let arrayLike = { // 인덱스와 length프로퍼티가 있음 => 유사 배열
      0: "Hello",
      1: "World",
      length: 2
    };
    // Symbol.iterator가 없으므로 에러 발생
    for (let item of arrayLike) {}
    ```

  - 문자열은 이터러블 하면서 유사배열이다.

- 이터러블과 유사배열은 배열이 아니기 때문에 배열메소드(`pop`같은거)를 사용하지 못합니다.

  - `Array.from(obj[, mapFn, thisArg])`을 통해서 배열로 만들어줍니다.

    - `mapFn`으로 요소를 추가하기전 함수를 적용할 수 있습니다.

    - ```js
      // 각 숫자를 제곱
      let arr = Array.from(range, num => num * num);
      alert(arr); // 1,4,9,16,25
      ```




## 맵과 셋

- `맵`은 객체와 유사하지만 키에 다양한 자료형을 허용합니다.

  - 객체와 배열과 다른점

    - 객체와 다르게 키값의 객체를 넣을 수 있다는 점이 중요합니다.
    - `맵`은 객체의 프로퍼티와 다르게 삽입된 순서를 기억합니다.
    - 배열처럼 내장 메서드 `forEach`를 지원합니다.

  - `new Map()` – 맵을 만듭니다.

  - `map.set(key, value)` – `key`를 이용해 `value`를 저장합니다.

    - ```js
      map.set('1', 'str1')
        .set(1, 'num1')
        .set(true, 'bool1'); // 체이닝이 가능합니다.
      ```

  - `map.get(key)` – `key`에 해당하는 값을 반환합니다. `key`가 존재하지 않으면 `undefined`를 반환합니다.

  - `map.has(key)` – `key`가 존재하면 `true`, 존재하지 않으면 `false`를 반환합니다.

  - `map.delete(key)` – `key`에 해당하는 값을 삭제합니다.

  - `map.clear()` – 맵 안의 모든 요소를 제거합니다.

  - `map.size` – 요소의 개수를 반환합니다.

  - `map.keys()` – 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환합니다.

  - `map.values()` – 각 요소의 값을 모은 이터러블 객체를 반환합니다.

  - `map.entries()` – 요소의 `[키, 값]`을 한 쌍으로 하는 이터러블 객체를 반환합니다. 이 이터러블 객체는 `for..of`반복문의 기초로 쓰입니다.

    - 객체를 통해서 `맵`을 만들고 싶다면 `Object.entries(obj)`를 사용하면 됩니다.

      - ```js
        let obj = {
          name: "John",
          age: 30
        };
        let map = new Map(Object.entries(obj));
        alert( map.get('name') ); // John
        ```

    - 반대로는 `Object.fromEntries(map.entries())`

      - `map.entries()`는 `map`으로 줄여도 됨

- `셋`

  - `new Set(iterable)` – 셋을 만듭니다. `이터러블` 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어줍니다.

  - `set.add(value)` – 값을 추가하고 셋 자신을 반환합니다.

  - `set.delete(value)` – 값을 제거합니다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 `true`, 아니면 `false`를 반환합니다.

  - `set.has(value)` – 셋 내에 값이 존재하면 `true`, 아니면 `false`를 반환합니다.

  - `set.clear()` – 셋을 비웁니다.

  - `set.size` – 셋에 몇 개의 값이 있는지 세줍니다.

  - 반복 작업은 `for of` `forEach`

    - ```js
      let set = new Set(["oranges", "apples", "bananas"]);
      for (let value of set) alert(value);
      
      set.forEach((value, valueAgain, set) => {
        alert(value);
      });
      ```

  - `set.keys()` – 셋 내의 모든 값을 포함하는 이터러블 객체를 반환합니다.

  - `set.values()` – `set.keys`와 동일한 작업을 합니다. `맵`과의 호환성을 위해 만들어진 메서드입니다.

  - `set.entries()` – 셋 내의 각 값을 이용해 만든 `[value, value]` 배열을 포함하는 이터러블 객체를 반환합니다. `맵`과의 호환성을 위해 만들어졌습니다.



## 위크맵과 위크셋

- 가비지 컬렉션이 일어나는 상황을 이용해서 `위크맵` 과 `위크셋`을 사용합니다.

  - 둘다 반복 작업이 불가능합니다.

- `위크맵`의 키는 반드시 객체이여야합니다.

  - 이는 서드파티 라이브러리 같은 외부코드에 있는 객체를 가지고 작업해야하는 경우 사용됩니다.

    - 객체가 있을때만 돌아가도록! 원할때는 쓰고 그외에는 삭제가되도록

    - 지속적으로 메모리를 비워주기 위함 (수동으로 지우기에는 골치아픔)

      - ```js
        // 📁 visitsCount.js
        let visitsCountMap = new WeakMap(); // 위크맵에 사용자의 방문 횟수를 저장함
        
        // 사용자가 방문하면 방문 횟수를 늘려줍니다.
        function countUser(user) {
          let count = visitsCountMap.get(user) || 0;
          visitsCountMap.set(user, count + 1);
        }
        ///////////////////////////////////////////////////
        // 📁 main.js
        let john = { name: "John" };
        countUser(john); // John의 방문 횟수를 증가시킵니다.
        console.log(visitsCountMap)
        // John의 방문 횟수를 셀 필요가 없어지면 아래와 같이 john을 null로 덮어씁니다.
        john = null;
        ```

    - 캐싱에서도 유용합니다.

- `위크셋`은 객체만 저장할 수 있습니다.

  - 복잡한 데이터를저장하지 않지만 사용자의 사이트 방문 여부를 추적하는 용도로 쓸수 있습니다.
    - 예 아니오 정도의 데이터



## 일반 객체 순회 메서드

- 일반 객체 순회 메서드

```js
let user = {
  name: "John",
  age: 30
};
```

- `Object.keys(user) = ["name", "age"]`

- `Object.values(user) = ["John", 30]`

- `Object.entries(user) = [ ["name","John"], ["age",30] ]`

- 심볼인 키는 무시합니다.

- `Object~~`를 쓰는 이유는 이터러블이 아닌 배열로 반환해줍니다.

- 객체에는 `map` `filter`를 사용하지 못합니다.

  - `Object.entries`와 `Object.fromEntries`는  사용가능!

    - `Object.entries(obj)`를 사용해 객체의 키-값 쌍이 요소인 배열을 얻습니다.

    - 1.에서 만든 배열에 `map` 등의 배열 전용 메서드를 적용합니다.

    - 2.에서 반환된 배열에 `Object.fromEntries(array)`를 적용해 배열을 다시 객체로 되돌립니다.

    - ```js
      let prices = {
        banana: 1,
        orange: 2,
        meat: 4,
      };
      let doublePrices = Object.fromEntries(
        // 객체를 배열로 변환해서 배열 전용 메서드인 map을 적용하고 fromEntries를 사용해 배열을 다시 객체로 되돌립니다.
        Object.entries(prices).map(([key, value]) => [key, value * 2])
      );
      alert(doublePrices.meat); // 8
      ```

      

## 구조 분해 할당

- 객체나 배열을 분해할수 있는 문법인 구조 분해 할당 이라는 것이 있습니다.

  - ```js
    // 이름과 성을 요소로 가진 배열
    let arr = ["Bora", "Lee"]
    
    // 구조 분해 할당을 이용해
    // firstName엔 arr[0]을
    // surname엔 arr[1]을 할당하였습니다.
    let [firstName, surname] = arr;
    
    alert(firstName); // Bora
    alert(surname);  // Lee
    ```

- 쉼표를 통해서 중간의 요소를 생략할 수 있습니다.

  - ```js
    // 두 번째 요소는 필요하지 않음
    let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
    
    alert( title ); // Consul
    ```

- 할당 연산자 우측엔 모든 이터러블이 올 수 있습니다.

  - 좌측에는 할당할 수 있는거라면 뭐든지 올수 있습니다.

- 순회에도 사용가능합니다.

  - ```js
    let user = {
      name: "John",
      age: 30
    };
    
    // 객체의 키와 값 순회하기
    for (let [key, value] of Object.entries(user)) {
      alert(`${key}:${value}`); // name:John, age:30이 차례대로 출력
    }
    
    ```

  - ```js
    let user = new Map();
    user.set("name", "John");
    user.set("age", "30");
    
    for (let [key, value] of user) {
      alert(`${key}:${value}`); // name:John, then age:30
    }
    ```

- 변수 교환이 가능합니다.

  - ```js
    let guest = "Jane";
    let admin = "Pete";
    // 변수 guest엔 Pete, 변수 admin엔 Jane이 저장되도록 값을 교환함
    [guest, admin] = [admin, guest];
    ```

- `...`으로 나머지 요소들을 가져올 수 있습니다. (가장 마지막에 있어야합니다.)

  - ```js
    let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
    
    alert(name1); // Julius
    alert(name2); // Caesar
    
    // `rest`는 배열입니다.
    alert(rest[0]); // Consul
    alert(rest[1]); // of the Roman Republic
    alert(rest.length); // 2
    ```

- 값이 없다면 `undefined`로 정해지면 미리 기본값을 설정할 수 있습니다.

  - ```js
    // 기본값
    let [name = "Guest", surname = "Anonymous"] = ["Julius"];
    ```

  - 기본값으로 함수도 할당될 수  있습니다. (표현식의 경우 유용)

- 객체 역시 분해가 가능합니다.

  - ```js
    let options = {
      title: "Menu",
      width: 100,
      height: 200
    };
    let {title, width, height} = options; //순서가 바뀌어도 결과는 값습니다.
    alert(title);  // Menu
    
    let {width: w, height: h=300, title=200} = options;
    alert(width); // 안먹힘
    alert(h);      // 200
    ```

- 주의해야할 점

  - ```js
    let title, width, height;
    
    // ()로 감싸주지않으면 {}를 코드블럭으로 인식해서 에러가 발생합니다.
    ({title, width, height} = {title: "Menu", width: 200, height: 100});
    
    alert( title ); // Menu
    ```

- 구조 분해는 함수의 복잡한 매개변수를 정리하는데 잘쓰인다

  - ```js
    let options = {
      title: "My menu",
      items: ["Item1", "Item2"]
    };
    
    function showMenu({
      title = "Untitled",
      width: w = 100,  // width는 w에,
      height: h = 200, // height는 h에,
      items: [item1, item2] // items의 첫 번째 요소는 item1에, 두 번째 요소는 item2에 할당함
    }) {
      alert( `${title} ${w} ${h}` ); // My Menu 100 200
      alert( item1 ); // Item1
      alert( item2 ); // Item2
    }
    
    showMenu(options);
    
    
    ```

  - 기본값 설정 방법

    - ```js
      function showMenu({ title = "Menu", width = 100, height = 200 } = {}) {
        alert( `${title} ${width} ${height}` );
      }
      
      showMenu(); // Menu 100 200
      ```




## Date 객체와 날짜 

Date객체는 날짜생성, 수정, 시간 측정 등등 시간에 관련한 용도로 사용할 수 있습니다.



- `new Date()` 

  - 인수가 없다면 현재 날짜와 시간이 반환됩니다.
  - `Mon Mar 28 2022 21:49:31 GMT+0900 (한국 표준시)`\

- `new Date(milliseconds)`

  - UTC 기준(UTC+0) 1970년 1월 1일 0시 0분 0초에서 `milliseconds` 밀리초(1/1000 초) 후의 시점
  - 1970년 기준으로 흘러간 밀리초의 정수를 `타임스탬프`라고 합니다.

- `new Date(datestring)`

  - 문자열을 넣게 되면 자동으로 구문 분석이 됩니다.

- `new Date(year, month, date, hours, minutes, seconds, ms)` 

  - 주어진 인수로 조합되어서 나타납니다.
    - `year`는 반드시 네 자리 숫자여야 합니다. `2013`은 괜찮고 `98`은 괜찮지 않습니다.
    - `month`는 `0`(1월)부터 `11`(12월) 사이의 숫자여야 합니다.
    - `date`는 일을 나타내는데, 값이 없는 경우엔 1일로 처리됩니다.
    - `hours/minutes/seconds/ms`에 값이 없는 경우엔 `0`으로 처리됩니다.

- `getFullYear()`

  - 연도(네 자릿수)를 반환합니다.
  - `getYear()`도 있지만 두 자리수를 반환할 수 있기 때문에 쓰면 안됩니다. 

- `getMonth()`

  - 월을 반환합니다(**0 이상 11 이하**).

- `getDate()`

  - 일을 반환합니다(1 이상 31 이하). 어! 그런데 메서드 이름이 뭔가 이상하네요.

- `getHours()`, `getMinutes()`, `getSeconds()`, `getMilliseconds()`

  - 시, 분, 초, 밀리초를 반환합니다.

- `getDay()`

  - 요일을 반환 합니다. ( 0: 일요일 1:월요일 ... 6: 토요일)

- 위 메소드들은 현지의 값으로 나타냅니다.

  -  `get` 옆에 `UTC` 같은걸 써줌으로서 바꿀수 있습니다.

- `getTime()`

  - 주어진 일시와 1970년 1월 1일 00시 00분 00초 사이의 간격(밀리초 단위)인 타임스탬프를 반환합니다.

- `getTimezoneOffset()`

  - 현지 시간과 표준 시간의 차이(분)를 반환합니다.

- 날짜 구성요소를 설정할 수 있습니다.

  - [`setFullYear(year, [month\], [date])`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setFullYear)

  - [`setMonth(month, [date\])`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setMonth)

  - [`setDate(date)`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setDate)

  - [`setHours(hour, [min\], [sec], [ms])`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setHours)

  - [`setMinutes(min, [sec\], [ms])`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setMinutes)

  - [`setSeconds(sec, [ms\])`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setSeconds)

  - [`setMilliseconds(ms)`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setMilliseconds)

  - [`setTime(milliseconds)`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/setTime) 
    - 1970년 1월 1일 00:00:00 UTC부터 밀리초 이후를 나타내는 날짜를 설정

- `date` 객체는 날짜범위를 넘어가면 자동으로 고쳐집니다. 

  - 초과되면 다음 시간으로 넘어 갑니다.

- 숫자로 형변환을 하면 타임스탬프로 변합니다.

  - ```js
    let date = new Date();
    alert(date); 
    //Mon Mar 28 2022 22:03:05 GMT+0900 (한국 표준시)
    alert(+date); // 타임스탬프(date.getTime()를 호출한 것과 동일함)
    //1648472602908
    ```

- `Date`객체를 만들지 않고 `Date.now()`를 사용하면 시차를 측정가능합니다.

  - 타임스탬프를 반환합니다.

  - 객체를 안만들기 때문에 가비지 컬렉터의 일을 도와줍니다.

  - ```js
    let start = Date.now(); // 1970년 1월 1일부터 현재까지의 밀리초
    // 원하는 작업을 수행
    for (let i = 0; i < 100000; i++) {
      let doSomething = i * i * i;
    }
    let end = Date.now(); // done
    alert( `반복문을 모두 도는데 ${end - start} 밀리초가 걸렸습니다.` ); // Date 객체가 아닌 숫자끼리 차감함
    ```

- `Date.parse(str)`

  - 문자열에서 날짜를 읽어올 수 있습니다.

  - 문자열의 형식은 `YYYY-MM-DDTHH:mm:ss.sssZ`처럼 생겨야 합니다.

    - `YYYY-MM-DD` – 날짜(연-월-일)

    - `"T"` – 구분 기호로 쓰임

    - `HH:mm:ss.sss` – 시:분:초.밀리초

    - `'Z'`(옵션) – `+-hh:mm` 형식의 시간대를 나타냄. `Z` 한 글자인 경우엔 UTC+0을 나타냄

    - `YYYY-MM-DD`, `YYYY-MM`, `YYYY`같이 더 짧은 문자열 형식도 가능합니다.

  - 형식이 맞지 않으면 `NaN` 을 출력합니다.



## JSON과 메서드



- 객체 데이터를 네트워크를 통해서 넘겨주려면 문자열로 변환해야합니다.

  - `toString`을 쓸수 있지만 수정을 해야된다면? 상당히 까다롭습니다.

- JSON은 값이나 객체를 나타내주는 범용 포맷입니다.

  - 자바스크립트에서 사용할 목적으로 만들어졌습니다.

  - JSON을 데이터 교환 목적을 사용하는 경우가 많습니다.

  - `JSON.stringify` 

    - 객체를 JSON으로 바꿔줍니다.
    - 원시값에도 적용이 가능합니다.
    - 반영이 안되는 프로퍼티도 있습니다.
      - 함수 프로퍼티
      - 심볼형 프로퍼티
      - 값이 `undefined`인 프로퍼티
      - 대부분 무시되어도 됩니다.
    - 순환 참조는 문자열로 바꾸지 못합니다.

  - `JSON.parse`

    - JSON을 객체로 바꿔줍니다.

    - ```js
      let value = JSON.parse(str, [reviver]);
      ```

      - str
        - JSON 형식의 문자열
      - reviver
        - 모든 `(key, value)` 쌍을 대상으로 호출되는 function(key,value) 형태의 함수로 값을 변경시킬 수 있습니다.

```js
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};

let json = JSON.stringify(student);

alert(typeof json); // 문자열이네요!

alert(json);
/* JSON으로 인코딩된 객체:
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
*/
```

- JOSN 통해 인코딩 된 객체는
  - 문자열은 큰따옴표로 감싸야합니다. 



- ```js
  let json = JSON.stringify(value[, replacer, space])
  ```

  - `replacer`를 쓰면 원하는 프로퍼티만 직렬화가 가능합니다.
    - JSON으로 인코딩 하길 원하는 프로퍼티가 담긴 배열.
    - 매핑 함수 `function(key, value)`
  - `space`에 숫자를 넣어주면 값만은 객체를 별도에 줄에 출력하고 공백은 2개 띄웁니다.(들여쓰기)
    - 가독성을 높여줍니다.

- 객체에 `toJSON` 메소드가 있으면 `JSON.stringify` 가 실행시 자동으로 호출해줍니다.

  - ```js
    let room = {
      number: 23
    };
    
    let meetup = {
      title: "Conference",
      date: new Date(Date.UTC(2017, 0, 1)),
      room
    };
    
    alert( JSON.stringify(meetup) );
    /*
      {
        "title":"Conference",
        "date":"2017-01-01T00:00:00.000Z",  // (1)
        "room": {"number":23}               // (2)
      }
    */
    ```

