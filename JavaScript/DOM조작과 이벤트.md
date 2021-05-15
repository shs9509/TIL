# 자바스크립트

자바스크립은 브라우저화면을 **동적**으로 만들어줌

지금  ES6+ 표준 으로 넘어옴



브라우저에서는 

DOM, BOM조작, ECMAScript 가능



## DOM (Document Object Model)

- 문서에 대한 모든 내용을 담고있는 객체. 도큐먼트에 관련 된 내용 모두

- 문서 즉 열려진 페이지에 대한 정보를 따로 객체화 시켜서 관리함



## DOM 조작

### 선택

- Document.querySelector()
  - 인자와 일치하는 엘리먼트 하나선택
  - css선택자 문법에 만족하는 첫번재 객체를 반환한다.
  - (sections)-> sections 태그를 가진 요소를 찾습니다.
  - (#sections) -> sections 아이디를 가진 요소를 찾습니다
  - (.section) -> section 클래스명을 가진 요소를 찾습니다
- Document.queryAll()
  - 인자와 일치하는 여러 엘리먼트 선택
  - 지정된 셀렉터에 일치하는 NodeList 반환
    - 노드리스트는 인덱스번호호만 각항목에 접근가능
    - 배열에사용하는 함수나 다양한 메서드 사용가능
  - html 컬렉션과 노드리스트
    - Live Collection으로 DOM변경사항을 실시간으로 반영
    - 근데 querySelectorAll()의 노드리스트는 정적
- getElementById()
- getElementByTagName()
- getElementByClassName()  
- 근데 이것들 안씀



- 맨위에 두개가 사용하기 유연하기 때문에 그걸씀

  

### 변경

- .createElement()

  - html 요소를 만들수있다.

- .append()

  - Node 객체와 문자열을 넣을수있다.
  - 다수의 요소를 한꺼번에 넣을수있다.
  - return 값이 없다. > undefine 나옴

  ```javascript
  console.log(docoument.body.append(div,'hello',p)); // undefined
  ```

- .appendChild()

  - Node 객체만 넣을수있다.
  - 한번에 한 요소만 넣을수있다.
  - return 값이 있다.

  ```javascript
  console.log(docoument.body.appendChild(div)); // div(Node object)
  ```

- .remove

- .removeChild()

- textContent

  - 노드의 모든 요소컨텐츠를 가져옴

- innerText

  \<li>가자\<li>

- innerHTML

  - 가자

- setAttribute(name, value)

  - 지정된 요소의 값을 설정

- getAttribute()

  - 해당요소의 지정된 값을 반환

- Node 객체 - Dom의 시조

  ![image-20210503222720382](C:\Users\ssej0\AppData\Roaming\Typora\typora-user-images\image-20210503222720382.png)



------------



### 이벤트

- 네트워크 활동, 사용저의 상호작용을 알림

- **"~하면 ~한다"** 를 설정한다.

이벤트 처리기

- EventTarget.addEventListener(type, listener)
  - type : 이벤트 유형
  - listener : 알림받는 객체

```javascript
btn.addEventListener('click', function(event){
	alert('버튼활성')
})
```

- removeEventListener()



---------









문서조작

문서가 구조화되어있고 이를 다 객체로 취급함

최상위객체- 윈도우 > 생략가능

window.document.title 이건 브라우저이름, 바꿀수도잇다. 

생긴걸보면 dom이트리모델인것을 이해할수있다.

document  페이지의 진입점

파싱-parsing 

- 구문분석, 해석

- 부라우저가 문자열을 해석해서 돔트리로 만드는과정

  



### BOM (Browser Object Model)

- 브라우저에 대한 모든 내용을 담고있는 객체. 브라우저에 관련 된 내용 모두

- 뒤로가기, 북마크, 즐겨찾기, 히스토리, URL정보 등..

- 브라우저가 가지고 있는 정보를 따로 객체화 시켜서 관리함

자바스크립트가 브라우저와 소통하기위한 모델

브라우저의 창이나 프레임을 추상화해서 프로그래밍적으로 제어할수있도록 제공



### 자바스크립코어

프로그래밍언어





자동으로 세미콜론이 삽입됨



변수식별자

대소문자 구별

클래스명 외에는 모두 소문자로 시작

카멜케이스 이용

