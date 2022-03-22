> https://ko.javascript.info/



- 자바스크립트란?

  - 웹페이지에서 동적이 이벤트를 보여주기 위해서 사용하는 프로그래밍 언어입니다.

- 자바스크립트로 작성한 프로그램은 `script`라고 합니다.

- 스크립트는 `HTML`에서 작성이되고 웹페이지를 불러오면 자동으로 실행됩니다.

- 자바스크립트는 브라우저 뿐만아니라 서버에서도 실행가능합니다. 

  - `Nodejs`

  - 또한 자바스크립트 엔진이 들어있는 모든 디바이스에서도 실행가능합니다.
    - 대표적으로 크롬의 `V8`

- 엔진의 동작방식은 어떤가요?

  1. 엔진이 스크립트를 읽고 (파싱)

  2. 이를 기계어로 변환합니다. (컴파일)

  3. 기계어가 된 코드가 실행되는 식으로 엔진이 동작합니다.

- 엔진은 각 단계마다 최적화를 진행합니다. 컴파일이후에도 기계어를 최적화 진행을 합니다.

- 자바스크립트는 브라우저에서 어떤일을 할수있죠?

  - 웹페이지 조작, 클라이언트와 서버의 상호작용에 관한 모든일을 할 수 있습니다.
    - 페이지에 새로운 요소 추가나 스타일 수정
    - 마우스 클릭같은 사용자 이벤트에 반응이 가능
    - 네트워크에 서버 요청이나 파일 다운,업로드
    - 쿠키를 가져오거나 `alert`
    - 로컬스토리지 사용

- 그럼 할 수 없는 일은요?

  - 보안과 관련해서 자바스크립트 제약을 갖고있습니다.
  - 디스크내 파일에 접근하는 것에 특정방식을 사용해야되며
  - 카메라 마이크 접근에 허가를 받아야합니다.
  - 브라우저에서 별개의 창과 탭끼리는 서로 정보를 공유하지 않습니다.
    - 한 창내에 있을경우는 예외
    - 또한 도메인이나 프로토콜, 포트가 다르면 페이지에 접근불가능 합니다.
      - 이 제약사항을 "동일출처정책" 이라고 합니다.
        - 이를 허가 하기 위해서는 두페이지의 교환에 동의하거나
        - 특수한 자바스크립트 코드가 필요합니다.
    - 이는 해당 페이지가 다른 페이지에 접근하여 개인정보를 훔치는 것을 막기위함입니다.
  - 페이지를 생성한 서버와 정보를 쉽게 주고받을 수 있지만 타사이트는 불가능합니다.
    - 여기는 원격서버에서 허가를 해줘야됩니다. (HTTP 헤더사용)

- 자바스크립트의 장점은 무엇인가요?

  - HTML 과 CSS를 통합할수 있다는점
  - 모든 주요 브라우저에서 지원하고 기본 언어롤 사용된다는 점



-----------



- 웹페이지에서 자바스크립트 코드를 추가하기 위해서는`script` 태그를 사용합니다.
  - HTML 내에서 `script`태그 내에서 코드를 입력하는 경우는 코드가 매우 간단할 때입니다.
    - 그외에는 `src`속성을 사용해서 js 파일을 불러와서 사용합니다.
    - 이러면 브라우저가 스크립트를 다운받아 캐시에 저장하기 때문에 성능상 이점도 있습니다.



--------



- 자바스크립트가 발전해오면서 옛날 코드와 호환성 문제를 없애기 위해서 strict모드가 활성화 되어있지 않습니다. 

- 하지만 `use strict`을 사용해서 모던 자바스크립트의 변경사항을 활성화해야합니다.

  - 스크립트 최상단에 써야합니다. 반드시

  - ```
    "use strict";
    ```

  - 이러게 작성하면 스크립트 전체가 "모던한" 방식으로 동작합니다.

  - 그런데 브라우저 콘솔에서창에서는 적용되지 않습니다.

    - 브라우저 콘솔창에서 쓰기위해서는 콘솔창에 `"use strict";` 적고 `shift+enter` 하고 코드를 이어서 쓰면 됩니다.

  - 근데 모던 자바스크립트에서 "모듈","클래스" 를 사용한다면 자동으로 적용됩니다.



-----------



- 객체는 참조에의해 저장되고 복사됩니다.

  - 값이 복사가되는게 아니라 참조값을 복사함

  - 값을 복사하고 싶으면 `for in`으로 순회해서 값을 넣거나

  -  `Object.assign(dest, [src1, src2, src3...])`을 씀

    - dest가 목표, src1는 복사하고자하는 객체

    - 여러개를 복사가능! 같은 프로퍼티가 있으면 덮어씌워짐

    - ```js
      let user = {
        name: "John",
        age: 30
      };
      let clone = Object.assign({}, user);
      ```

    - 근데 얕은 복사일뿐 깊은복사는 lodash의 `_.cloneDeep(obj)`를 씀

  - 또는 전개연산자를 사용하면된다.

    - 전개연산자 특징은 1depth로 만들어준다.

    - ```js
      const arr = [1,2,3];
      let test_arr = [4,5,6];
      let test_arr2 = [4,5,6];
      //ES6
      test_arr2.push(...arr);
      console.log(test_arr2); //[4, 5, 6, 1, 2, 3]
      ```

      

------------



- 함수형 프로그래밍에서 변숫값 변경을 금합니다.
- 변수명에 특수기호는 반드시 `$` 와 `_` 만 허용됩니다.
- 대소문자를 구별합니다.
- 변수명 선언에는 대부분 카멜 기법을 사용합니다.
- 예약어는 사용금지 합니다.

- `const`는 상수입력에 사용됩니다.
  - 대문자 상수를 이용하는 것은 널리 사용되는 관습입니다.
  - 대문자 상수는 하드코딩한 값을 쓸때 사용됩니다.
    - 예시 `#FF231` 색상같은거
- 변수를 재사용하는 것은 디버깅에 큰 시간을 들게 합니다. 변수 선언을 통해 새로 만듭시다
  - 모던 자바스크립트 압축기와 브라우저는 코드최적화를 잘해줍니다!



----------



- 자바스크립트는 동적타입언어이다. 변수에 저장되는 값에 따라 타입이 변경된다는 것이다.
- 타입은 8가지의 기본 자료형을 갖고있습니다.
- `Number` `숫자형`을 다룰 때 에러상황이 나타난다면 `NaN`을 반환됩니다.
- `BigInt`는 아주 큰숫자를 나타내기위해서 길이에 상관없이 정수를 나타내줍니다.
  - `214234234n` 숫자 뒤에`n`이 붙으면 `BigInt`형입니다.
  - 많이 사용되지는 않지만 암호관련 작업에 사용됩니다.

- `string` `문자형`은 백틱(`) 사이에 ${} 를 통해서 변수나 표현식을 넣을 수 있습니다.
- `불린형` 은 `true` 와 `false` 만 존재합니다.
- `null` 은 값이 없음을 나타냅니다.
  - 출력시 `object`입니다. 이것은 언어자체의 버그입니다.
- `undefined` 은 값이 아직 할당되지 않았음을 나타냅니다. 하지만 직접적으로 할당하진 않습니다.
- `객체형`은 복잡한 개체를 표현할수있습니다. 위의 원시자료형과는 다릅니다.
  - 함수는 객체형에 속합니다. type이`function`으로 나오는 것은 오래된 규칙입니다.
- `심볼`은 객체의 고유한 식별자를 만들때 사용됩니다.



-----------------------



- `alert`는 모달창을 생성합니다. 모달창 이외의 것과는 상호작용이 불가능 합니다.

- `prompt` 는 메세지, 입력필드, 확인, 취소있는 모달창을 생성합니다.

  - ```js
    let result = prompt(title:메세지, [default:초기값]);
    ```

  - `[]`는 필수가 아닌 선택값이란 뜻

  - 입력취소하면 `null`이 반환되고 확인이되면 입력된 문자열이 반환됩니다.

  - IE 를 위해서 기본값을 넣어줍시다.

- `confirm`은 매개변수로 받은 질문과 확인 취소가 있는 모달창을 생성합니다.

  - 확인을 누르면 `true` 가 취소면 `false`가 반환됩니다.

  - ```js
    let result = confirm('남자입니까?')
    ```



-----------



- 자바스크립트는 암묵적으로 형변환이 진행됩니다.
- 빈문자열 `""` 과 숫자 `0` 은 불린에서 `false`로 변환됩니다.
- 숫자의 경우 
  - `null`은  `0` 
  - `undefined`는 `NaN` 입니다. 
  - `string`의 경우 처음과 끝의 공백을 제외하면서 변환됩니다.
  - `\t` `\n` 은 길이가 0인 문자열로 취급되므로 숫자 `0`이 됩니다.



---------



- `+` 연산자가 다른 연산자와 다른점은 피연산자로 `string`이 있는경우 따라서 형변환이 일어난다는 점입니다.

  - 나머지는 숫자로 변환됨

  - ```
    alert(2+2+'1') // 41 이 출력된다.
    alert("2"+2+1) // 221 이 출력된다.
    alert(2-1-"1") // 0 이 출력된다.
    ```

- `,`쉼표 연산자는  코드를 짧게 쓰기위한 의도이고 마지막 표현식의 평가 결과감 반환됩니다.

  - ```
    // 한 줄에서 세 개의 연산이 수행됨
    for (a = 1, b = 3, c = a * b; a < 10; a++) {...}
    ```

  - 이런식으로 사용됩니다. 그런데 가독성이 좋지않아 진짜 필요한 경우에만 씁시다.



--------



- 문자열 비교시 유니코드 순으로 따지고 길이순으로 따집니다. 
  - 'a' > 'A' 입니다.
  - 숫자랑 비교시에는 변환이 진행됩니다.
- `==` 는 `0`과 `false`를 구별하지 못합니다.
  - 그래서 `===`를 사용하면 형변환 없이 비교를 진행합니다.

- `==`는 `null`과 `undefined`를 같다고 비교합니다.
  - 이는 특수한 케이스이며 `null`과 `undefined`는 `==` 사용 시 형변환을 거치지 않습니다.
  - 그래서 무조건 `false`를 출력합니다.



-----------



- `&&`는 `||`보다 우선순위가 높습니다.
- `!!`를 씀으로서 `불린형`으로 만들 수 있습니다.



---------------



- `nullish` `??`
  -  `a ?? b` a가 `null`도 아니고 `undefined`도 아니면`a`이고 그외에는 `b`이다.
  - `||` 와의 차이는 반환값의 차이입니다.



----------------



- `?` 사용에는 `break`, `continue`를 사용할수없습니다. `if`를 씁시다.



-------



- 반복문 사용시 원하는 곳으로 `break`, `continue`를 하고 싶다면 `label`을 사용하면됩니다.

  - ```js
    here: for(let i=3; i<4; i++){
        for (let j=3; j<4; j++){
            if (i>j){
                break here; //이럼 here 위치로 break가 일어남 아예밖으로 나오게됨
            }
        }
    }
    ```





-----------



- 스크립트 내에서 `debugger;` 를 사용하면 중단점을 설정한 것 과은 효과를 낸다.



-----------



- 유명한 자바스크립트 스타일 가이드
  - [Google의 자바스크립트 스타일 가이드](https://google.github.io/styleguide/jsguide.html)
  - [Airbnb의 자바스크립트 스타일 가이드](https://github.com/airbnb/javascript)
  - [Idiomatic.JS](https://github.com/rwaldron/idiomatic.js)
  - [StandardJS](https://standardjs.com/)

- Linter를 사용하면 코드가 스타일 가이드를 준수하고있는지 자동으로 확인할 수 있다.

  - 오타 등 버그도 확인이 가능해서 좋다.

  - [JSLint](http://www.jslint.com/) – 역사가 오래된 linter

  - [JSHint](http://www.jshint.com/) – JSLint보다 세팅이 좀 더 유연한 linter

  - [ESLint](http://eslint.org/) – 가장 최근에 나온 linter

    1. [Node.js](https://nodejs.org/)를 설치합니다.

    2. npm(자바스크립트 패키지 매니저)을 사용해 다음 명령어로 ESLint를 설치합니다. `npm install -g eslint`

    3. 현재 작성 중인 자바스크립트 프로젝트의 루트 폴더(프로젝트 관련 파일이 담긴 폴더)에 `.eslintrc`라는 설정 파일을 생성합니다.

    4. 에디터에 ESLint 플러그인을 설치하거나 활성화합니다. 주요 에디터들은 모두 ESLint 플러그인을 지원합니다.

  - 설치방법: http://eslint.org/docs/user-guide/getting-started



----------



- 좋은 주석
  - 아키텍처를 설명하는 주석
    - 컴포넌트의 개요, 컴포넌트 간의 상호작용에 대한 설명
    - 상황에 따른 제어흐름
  - 함수 용례와 매개변수 정보를 담고 있는 주석
    - JSDoc 을 사용하면 함수에 관한 문서를 쉽게 작성이 가능하다.
  - 왜 이런방법으로 문제를 해결했는지를 설명하는 주석
    - 이미 햇던 방법을 새로 시도하게 만들지 않는것만으로 충분하다.
    - 최근 redux로 상태관리했으나 결국 로컬스토리지 사용을 하는게 나았다는게 떠오름..
  - 미묘한 기능이 있고 이기능이 어디에쓰이는지 설명하는 주석
- 안좋은 주석
  - 코드가 어떻게 동작하는지
  - 코드가 상세하게 무엇을 하는지



------------



- BDD 방법론
  - 테스트, 문서, 예시를 한데 모아놓은 개념

- BDD 명세서(spec)

```js
describe("pow", function() { //describe 첫 인수 - 구현하는 기능(title), 
  it("주어진 숫자의 n 제곱", function() { //it 첫 인수 -유스케이스설명, 테스트함수
    assert.equal(pow(2, 3), 8);//assert가 함수가 예상대로 동작하는지 확인 equal사용되서 8과 같은지 비교할것임
  });
});// 테스트마다 it 블록을 생성해서 진행
```



- 개발 순서

  1. 명세서 초안을 작성합니다. 초안엔 기본적인 테스트도 들어갑니다.

  2. 명세서 초안을 보고 코드를 작성합니다.

  3. 코드가 작동하는지 확인하기 위해 [Mocha](http://mochajs.org/)라 불리는 테스트 프레임워크를 사용해 명세서를 실행합니다.(Mocha에 대해선 아래에서 다룰 예정입니다.) 이때, 코드가 잘못 작성되었다면 에러가 출력됩니다. 개발자는 테스트를 모두 통과해 에러가 더는 출력되지 않을 때까지 코드를 수정합니다.

  4. 모든 테스트를 통과하는 코드 초안이 완성되었습니다.

  5. 명세서에 지금까진 고려하지 않았던 유스케이스 몇 가지를 추가합니다. 테스트가 실패하기 시작할 겁니다.

  6. 세 번째 단계로 돌아가 테스트를 모두 통과할 때까지 코드를 수정합니다.

  7. 기능이 완성될 때까지 3~6단계를 반복합니다.

- 사용되는 라이브러리
  - [Mocha](http://mochajs.org/) – 핵심 테스트 프레임워크로, `describe`, `it`과 같은 테스팅 함수와 테스트 실행 관련 주요 함수를 제공합니다.
  - [Chai](http://chaijs.com/) – 다양한 assertion을 제공해 주는 라이브러리입니다. 우리 예시에선 `assert.equal` 정도만 사용해 볼 예정입니다.
  - [Sinon](http://sinonjs.org/) – 함수의 정보를 캐내는 데 사용되는 라이브러리로, 내장 함수 등을 모방합니다. 본 챕터에선 사용하지 않고, 다른 챕터에서 실제로 사용해 볼 예정입니다.

```html
<!DOCTYPE html>
<html>
<head>
  <!-- 결과 출력에 사용되는 mocha css를 불러옵니다. -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.css">
    
  <!-- Mocha 프레임워크 코드를 불러옵니다. -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.js"></script>
  <script>
    mocha.setup('bdd'); // 기본 셋업
  </script>
    
  <!-- chai를 불러옵니다 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/chai/3.5.0/chai.js"></script>
  <script>
    // chai의 다양한 기능 중, assert를 전역에 선언합니다.
    let assert = chai.assert;
  </script>
</head>

<body>

  <script>
    function pow(x, n) {
      /* 코드를 여기에 작성합니다. 지금은 빈칸으로 남겨두었습니다. */
    }
  </script>

  <!-- 테스트(describe, it...)가 있는 스크립트를 불러옵니다. -->
  <script src="test.js"></script>

  <!-- 테스트 결과를 id가 "mocha"인 요소에 출력하도록 합니다.-->
  <div id="mocha"></div>

  <!-- 테스트를 실행합니다! -->
  <script>
    mocha.run();
  </script>
</body>

</html>
```



- 함수 `before`는 (전체) 테스트가 실행되기 전에 실행되고, 함수 `after`는 (전체) 테스트가 실행된 후에 실행됩니다. 함수 `beforeEach`는 *매* `it`이 실행되기 전에 실행되고, 함수 `afterEach`는 *매* `it`이 실행된 후에 실행됩니다.
  - `beforeEach/afterEach`와 `before/after`는 대개 초기화 용도로 사용됩니다. 카운터 변수를 0으로 만들거나 테스트가 바뀔 때(또는 테스트 그룹이 바뀔 때)마다 해줘야 하는 작업이 있으면 이들을 이용할 수 있습니다.

- BDD의 핵심은 실패할 수밖에 없는 테스트를 추가하고, 테스트를 통과할 수 있게(에러가 발생하지 않게) 코드를 개선하는 것이다.



------------



주목할 만한 폴리필

- [core js](https://github.com/zloirock/core-js) – 다양한 폴리필을 제공합니다. 특정 기능의 폴리필만 사용하는 것도 가능합니다.
- [polyfill.io](http://polyfill.io/) – 기능이나 사용자의 브라우저에 따라 폴리필 스크립트를 제공해주는 서비스입니다.



---------



- 객체에는 다양한 데이터를 담을 수 있음

- 프로젝트를 삭제하려면 `delete`를 사용한다.

- `const`로 수정된 객체는 수정이 가능합니다.

- 유효한 변수 식별자를 포함하는데 대괄호 표기법을 사용하기도 합니다.

  - ```js
    user["likes birds"] = true;
    ```

  - 안에 변수는 따옴표로 묶어줘야합니다.

- 객체 안에 프로퍼티가 대괄호로 둘러싸인것을 계산된 프로퍼티라고 한다.

  - ```js
    let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");
    
    let bag = {
      [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옵니다.
    };
    
    alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됩니다.
    ```

  - `[fruit]`의 프로퍼티 이름은 `fruit`에서 갖고 오겠다는 말 

  - ```js
    let fruit = 'apple';
    let bag = {
      [fruit + 'Computers']: 5 // bag.appleComputers = 5
    };
    ```

  - 복잡한 이름선정이 필요하게되면 대괄호표기법을 사용하게된다.

- 프로퍼티값을 편하게 선정해주는 단축구문을 사용할수잇다.

  - ```js
    let user = {
      name,  // name: name 과 같음
      age: 30
    };
    ```

- 프로퍼티에는 예약어를 사용해도 된다.

- `__proto__`는 근본이 있는 예약어라 객체 프로퍼티로 만들수 없다.

- 프로퍼티의 여부 확인은 `in`을 사용한다.

  - ```js
    let user = { name: "John", age: 30 };
    
    alert( "age" in user ); // user.age가 존재하므로 true가 출력됩니다.
    ```

  - 따옴표를 꼭 사용하자.

  - `in`을 안쓰면 `undefined`를 확인하는 방법이 있는데 이는 불확실한 방법이다.

- `for in`을 사용해서 객체의 모든 키를 순회 할수있습니다.

  - ```js
    let user = {
      name: "John",
      age: 30,
      isAdmin: true
    };
    
    for (let key in user) {
      // 키
      alert( key );  // name, age, isAdmin
      // 키에 해당하는 값
      alert( user[key] ); // John, 30, true
    }
    ```

  - 출력되는 프로퍼시는 시간순이지만 정수프로퍼티의 경우에는 정렬되어서 나타난다.



---------





- 객체프로퍼티에 할당된 함수를 `메서드`라고 함

- 이미 정의된 함수를 가지고 메서드로 등록할 수 있다.

  - ```js
    let user = {
      // ...
    };
    // 함수 선언
    function sayHi() {
      alert("안녕하세요!");
    };
    // 선언된 함수를 메서드로 등록
    user.sayHi = sayHi;
    user.sayHi(); // 안녕하세요!
    ```

- 메서드에서 단축구문이 존재한다.

  - ```js
    let user = {
        sayHi() {
            alert("안녕하세요!");
    	}
    };
    ```

- 메서드 내부에서 `this`를 사용해서 객체에 접근이 가능합니다. 

  - `this`는 메소드를 호출할때 사용된 객체를 나타냅니다. (점앞에 객체가 뭔지에 따라 결정 됨)
  - `this`를 안쓰고 그냥 객체를 참조해서 사용할수도있지만 이경우 다른 변수와 겹치는 상황이 생길수 있습니다.

- `this`의 값은 런타임에서 결정되기 때문에 컨텍스트에 다라 달라진다.

- `strict` 모드에서는 객체가 없을 경우 `undefined`가 호출됩니다.

  - 아닐 경우 `window`를 참조하게 됩니다.

- 화살표 함수는  고유한 `this`를 가지지않고 `평범함`외부 함수에서 `this`값을 가져옵니다. 

  - ```js
    let user = {
        firstName: "보라",
        sayHi() {
            firstName: "미래";
        	let arrow = () => alert(this.firstName);
        	arrow();
    	};
    };
    user.sayHi(); // 보라
    ```

  - `arrow`에서 `this`는 외부 함수 `user.sayHi()`의 `this`가 됩니다.

  - 외부 컨텍스트에 있는 `this`가 필요하면 화살표함수를 사용하면 됩니다.



------



- 유사한 여러객체는 만드는데 `new`를 사용하면 된다. +함수의 첫글자는 대문자를 사용해야한다. 이를 생성자 함수라고 한다.

  - `new`를 통해서 객체를 만들게되면
    - 처음에는 빈객체를 만들어서 `this`에 할당합니다.
    - 함수 본문을 실행하면서 `this` 프로퍼팅에 생성되면서 수정됩니다.
    - `this`를 반환합니다.

- 생성자의 의의는 재사용할 수 있는 객체 생성 코드를 구현하는 것이다.

- 모든 함수는`new` 붙어서 생성자 함수가 될 수 있습니다.

- 재사용필요없는 복잡한 객체를 생성할때는 익명 생성자함수를 만들면 됩니다.

  - ```js
    let user = new function() {
      this.name = "John";
      this.isAdmin = false;
    
      // 사용자 객체를 만들기 위한 여러 코드.
      // 지역 변수, 복잡한 로직, 구문 등의
      // 다양한 코드가 여기에 들어갑니다.
    };
    ```

- `new.target` 프로퍼티를 사용하면 함수가 `new`와 함꼐 호출되었는지 확인이 가능합니다.

  - 일반 호출을 하게되면 `undefined`를 호출하고 생성자 함수 호출을 하면 함수 자체를 반환합니다.

  - ```js
    function User() {
      alert(new.target);
    }
    
    // 'new' 없이 호출함
    User(); // undefined
    
    // 'new'를 붙여 호출함
    new User(); // function User { ... }
    ```

- 객체를 만드는 경우에도 `new`를 생략하면 코드가 정확히 무슨 일을 하는지 알기 어려우니깐 무조건 쓰자

- 생성자 함수에 `return`이 있는 경우`this`대신에 반환이 됩니다.

  - 원시형을 반환하면 `return`은 무시됩니다.



----------------------



- 옵셔널 체이닝 `?.`  프로퍼티가 없는 중첩객체를 에러 없이 접근이 가능하다.

- `?.`은 `?.`'앞’의 평가 대상이 `undefined`나 `null`이면 평가를 멈추고 `undefined`를 반환합니다.

  - 즉, 없음 말고 이다.
  - 에러가 발생안하는 점이 좋다.
  - 앞 평가대상에만 적용됩니다.

- `.`대신 대괄호 `[]`를 사용해 객체 프로퍼티에 접근하는 경우엔 `?.[]`를 사용할 수도 있습니다.

  - ```js
    let user1 = {
      firstName: "Violet"
    };
    
    let user2 = null; // user2는 권한이 없는 사용자라고 가정해봅시다.
    
    let key = "firstName";
    
    alert( user1?.[key] ); // Violet
    alert( user2?.[key] ); // undefined
    
    alert( user1?.[key]?.something?.not?.existing); // undefined
    ```

- 삭제는 가능하지만 할당은 불가능 합니다.

  - `undefined`에 값이 할당될수있기 때문

- `obj?.prop` – `obj`가 존재하면 `obj.prop`을 반환하고, 그렇지 않으면 `undefined`를 반환함

- `obj?.[prop]` – `obj`가 존재하면 `obj[prop]`을 반환하고, 그렇지 않으면 `undefined`를 반환함

- `obj?.method()` – `obj`가 존재하면 `obj.method()`를 호출하고, 그렇지 않으면 `undefined`를 반환함



-------------



- 자바스크립트는 객체 프로퍼티 키로 오직 문자형과 심볼형만 허용합니다.

- 유일한 식별자를 만들 때 사용합니다.

  - ```js
    let id = Symbol('id'); //'id'라는 설명이 붙은 심볼 id 가 생성
    ```

  - 유일성이 보장되기 때문에 여러개를 만들어도 값은 다릅니다.

  - 설명은 아무 영향이없습니다.

- 암묵적으로 타입 변환이 일어나지 않습니다.

- 출력을 위해서는 `.toString()`을 사용합니다.

  - ```js
    id.toString(); //Symbol(id)
    ```

- `.description`을 사용하면 설명만 확인이 가능합니다.

- 심볼을 사용하면 '숨김'프로퍼티를 만들수 있습니다.

  - 이는 외부코드에서 접근이 불가능하고 값도 덮어 쓸 수 없습니다.

  - ```js
    let user = { // 서드파티 코드에서 가져온 객체
      name: "John"
    };
    let id = Symbol("id");
    user[id] = 1;
    alert( user[id] ); // 심볼을 키로 사용해 데이터에 접근할 수 있습니다.
    ```

    - 서드파티에서 코드를 가져왔고 자신만의 건드릴수없는 식별자를 넣을수잇다.
    - 각 환경에서 심볼을 활용해서 식별자를 만들면 이름이 같아도 충돌이 나지않는다.  
    - 심볼로 안만들고 문자열로 만든다면 충돌이 일어난다.

- 객체 리터럴에서 심볼을 만드는 경우 `[]`를 이용한다.

  - ```js
    let person = {
        name : 'john',
        age : 15,
        [id] : 123
    }
    ```

- 심볼은 `for in`에서 배제됩니다.

  - '심볼형 프로퍼티 숨기기(hiding symbolic property)'라 불리는 이런 원칙 때문에 접근이 불가능합니다.

- [Object.assign](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)은 키가 심볼인 프로퍼티를 배제하지 않고 객체 내 모든 프로퍼티를 복사합니다.

  - 의도된것입니다.

  - ```js
    let id = Symbol("id");
    let user = {
      [id]: 123
    };
    
    let clone = Object.assign({}, user);
    alert( clone[id] ); // 123
    ```

- 전역 심볼이 필요한 경우도 있기 때문에  *전역 심볼 레지스트리(global symbol registry)*가 있습니다.

  - 전역 심볼 레지스트리 안에 심볼을 만들고 해당 심볼에 접근하면

    - 이름이 같은 경우 항상 동일한 심볼을 반환해줍니다.

  - ```js
    // 전역 레지스트리에서 심볼을 읽습니다.
    let id = Symbol.for("id"); // 심볼이 존재하지 않으면 새로운 심볼을 만듭니다.
    // 동일한 이름을 이용해 심볼을 다시 읽습니다(좀 더 멀리 떨어진 코드에서도 가능합니다).
    let idAgain = Symbol.for("id");
    // 두 심볼은 같습니다.
    alert( id === idAgain ); // true
    ```

  - `Symbol.keyFor(sym)`을 사용하면 심볼을 통해서 이름검색이 가능합니다. (전역심볼만!)

    - ```js
      // 이름을 이용해 심볼을 찾음
      let sym = Symbol.for("name");
      // 심볼을 이용해 이름을 얻음
      alert( Symbol.keyFor(sym) ); // name
      ```

    - 일반 심볼에서 이름을 얻고 싶다면 `description`을 사용하면됩니다.

      - ```js
        alert( localSymbol.description );
        ```



-----------



1. 객체는 논리 평가 시 `true`를 반환합니다. 단 하나의 예외도 없죠. 따라서 객체는 숫자형이나 문자형으로만 형 변환이 일어난다고 생각하시면 됩니다.
2. 숫자형으로의 형 변환은 객체끼리 빼는 연산을 할 때나 수학 관련 함수를 적용할 때 일어납니다. 객체 `Date`끼리 차감하면(`date1 - date2`) 두 날짜의 시간 차이가 반환됩니다. `Date`에 대해선 [Date 객체와 날짜](https://ko.javascript.info/date)에서 다룰 예정입니다.
3. 문자형으로의 형 변환은 대개 `alert(obj)`같이 객체를 출력하려고 할 때 일어납니다.

- 특수 객체 메서드를 사용하면 숫자형이나 문자형으로의 형 변환을 원하는 대로 조절할 수 있습니다.

- 객체 형 변환은 세종류로 나눠지도 'hint'로 불리는 값이 구분 기준이 됩니다.

  - 'hint'는 목표로 하는 자료형 이라고 생각하자
  - `string` : alert같은 문자열을 기대할때
  - `number` : 수학연산 적용하려고 할때
  - `default` : 흔하지는 않은데 획실치 않을때
  - 각 상황에 맞춰서 hint가 정의 되고 변환이 됩니다.

- ```js
  obj[Symbol.toPrimitive] = function(hint) {
    // 반드시 원시값을 반환해야 합니다.
    // hint는 "string", "number", "default" 중 하나가 될 수 있습니다.
  };
  
  //실사용
  let user = {
    name: "John",
    money: 1000,
  
    [Symbol.toPrimitive](hint) {
      alert(`hint: ${hint}`);
      return hint == "string" ? `{name: "${this.name}"}` : this.money;
    }
  };
  
  // 데모:
  alert(user); // hint: string -> {name: "John"}
  alert(+user); // hint: number -> 1000
  alert(user + 500); // hint: default -> 1500
  ```

- `toString`과 `valueOf`는 심볼이 생기기 이전부터 존재해 왔던 ‘평범한’ 메서드입니다. 이 메서드를 이용하면 '구식’이긴 하지만 형 변환을 직접 구현할 수 있습니다.

  - 에러라는게 확립되지않아서 원시자료형을 반환 안해도 에러가 안뜹니다.

  - hint가 'string’인 경우: `toString -> valueOf` 순(`toString`이 있다면 `toString`을 호출, `toString`이 없다면 `valueOf`를 호출함)

  - 그 외: `valueOf -> toString` 순

  - ```js
    let user = {
      name: "John",
      money: 1000,
    
      // hint가 "string"인 경우
      toString() {
        return `{name: "${this.name}"}`;
      },
    
      // hint가 "number"나 "default"인 경우
      valueOf() {
        return this.money;
      }
    
    };
    
    alert(user); // toString -> {name: "John"}
    alert(+user); // valueOf -> 1000
    alert(user + 500); // valueOf -> 1500
    ```



------------



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



------



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



-----------



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



---------



- 배열의 자료형에는 제양이 없습니다.
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
- 배열에는 `toString`이 구현되어있어서 출려갛면 문자열이 나옵니다.



----------



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

- `forEach` 인수로 주어진 함수를 배열 요소에 적용 가능

  - ```js
    ["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
      alert(`${item} is at index ${index} in ${array}`);
    });
    ```




- 배열 내 객체를 찾을 때에는 `find`를 사용한다.

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

- `find`는 하나의 요소만 찾는다. 여러개를 찾으려면 `filter`를 사용한다.

  - 배열을 반환한다. 



- `map`은 배열 요소 전체를 대상으로 함수를 호출하고 결과를 배열로 반환해줍니다.

  - ```js
    let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
    alert(lengths); // 5,7,6
    ```

- `sort` 배열의 요소를 정리를 하는데 요소안의 값은 문자열로 취급됩니다.

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



----------------



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

      

------------



























