## 비동기식 프로그래밍

자바스크립트는 **싱글스레드 언어**입니다. 그래서 한번에 한가지 일밖에 못합니다.

그런데 요즘 웹페이지에서는 동시에 일어나는 일이 많은데 희한합니다.

이처럼 동시에 여러가지 일을 하게 해주기 위해서 **비동기 프로그래밍** 을 진행합니다.



- 동기
  - 순차적 태스크 수행
  - 요청을 보내고 응답을 받아야함 다음동작이 이루어짐(blocking)


- 비동기

  - 병렬적 태스크  수행
  - 요청을 보내고 응답을 기다리지 않고 다음동작이 이루어짐(non-blocking)

  - 왜 비동기 선호? > 사용자경험을 위해 (기다리기가 싫다!)


- thread

  - 프로그램이 작업을 완료하는데 사용할수있는 단일프로세스

  - 각 스레드는 한번에 하나작업을 한다.

  - cpu가 여러개면 여러개의 일을 처리가능



### 이벤트 루프에 기반한 동시성(Concurrency) 모델

- call stack

  요청이 들어올떄마다 요청을 처리하는 스택형태의 자료구조

- web API

  브라우저영역에서 제공하는 API (DOM, AJAX, timeout 등)

- 태스크 큐

  콜백함수가 대기하는큐 형태의 자료구조

- 이벤트 루프

  콜스택이 비어있는지 확인

- 정리

  - 이벤트를 처리하는 Call Stack이 하나인 언어


  - 즉시처리못하는 이벤트를 **Web API**로 보내고 처리

    처리된이벤트는 순서대로 **Task Q**에 넣고

    **Call stack**이 비면 **Event Loop**가 옮겨줌 

- example

  - 콜백함수와 지연시간을 setTimeout 콜에 넘깁니다. 
    - 애초에 setTimeout 은 Web에서 API로 제공됨 v8에는 코드가 없음!

  - 브라우저가 타이머 실행함고

  - 모든 Web API는 작동이 완료된 콜백을 task queue 에 넣습니다.

  - 이벤트 루프는 콜스택과  task queue 를 주시하면서 콜스택이 비어있으면은 큐에 있던 콜백을 스택에 넣습니다.

- 상황

  - 콜스택에 쌓게되면 일단 느림 그리고 스레드를 다 쓰고있기에 중간에 렌더는 진행이안됨 하지만 비동기프로그래밍으로 하면 그만큼 빠르고 중간중간 렌더도 진행이된다.

  - 스크롤이벤트는 매프레임마다 진행됨 스크롤할때마다 어떤일을하면 큐에 잔뜩 쌓이는 경우가 생길수있음  그럼 콜스택에 쌓이는건 아니지만 프로세싱에 시간이 걸린다.



### 콜백함수

다른 함수에 인자로 함수가 들어가는걸 콜백함수라고 함

비동기 처리로 인해 생기는 문제들(값이 바로 불러와짐!)을 조절하기위해서 콜백함수를 사용함

순서를 정하는 것임!!

```js
function getData() {
	var tableData;
	$.get('https://domain.com/products/1', function(response) {
		tableData = response;
	});
	return tableData; //값을 불러오기도 전에 리턴해버림
}

console.log(getData()); // undefined
```

```js
function getData(callbackFunc) {
	$.get('https://domain.com/products/1', function(response) {
		callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
	});
}

getData(function(tableData) {
	console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
```



### 순차적인 연쇄 비동기작업

- 콜백안에 콜백을부르고 계속 부름

- 콜백지옥, 파멸의 피라미드

해결

- 비동기 콜백방식
  - 함수(콜백함수)  > 순서를 직접작성해줌
  - addEventListner() 의 두번째 인자 : 이벤트가 일어나면 ~~를 할거야
- promise-style
  - 콜백함수의 다음 표현



### Promise

자바스크립트는 비동기처리가 가능하다.

\> 그런데 일을 넘겨주는 웹 API에서 순차적인 일처리가 안된다

\> 그래서 콜백함수를 사용한다.

\>그런데 콜백지옥, 가독성이 떨어지는 코드가 생성된다.

\> 결국 Promise 라는 표현을 이용하게 된다.



[비동기작업].then(콜백)  - 성공하면 콜백

​	.then을 연속적으로 사용해서 연쇄적인 사용가능

[비동기작업].catch(콜백) - 실패하면 콜백

.finally - 실패 성공 상관없이 콜백시행, 어떠한 인자도 안받음 결과가 상관없으니

코드중복방지를 위해 사용



### axios

브라우저를 위한 promise  기반의 클라이언트

요청에 특화

```javascript
const request = new XMLHttpRequest() //생성하고
const url = 'http://~~'	// 데이터를 얻어올 url

request.open('GET',url) // 데이터를 준비하고
request.send()	// 요청보내기

const data = request.response// 받은응답
console.log(data) //근데 응답안온채로 출력한거라 아무것도안뜸 (스레드가 한개라)
```

```javascript
axios.get(url) //프로미스리턴
    .then(function (response){
    console.log(data)
})
    .catch() // 이렇게 깔끔해짐
```



현재 페이지를 자바스크립트를 통해서 동적으로 만들기

{% block script %}와 \<script> 를 설정하고

쿼리셀렉터로 폼이나 버튼 등을 선택하고

변경작업을 한다.

그리고 선택한 부분 이벤트에 대해서 axios를 한다.



--------

https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/#%EC%BD%9C%EB%B0%B1-%EC%A7%80%EC%98%A5-callback-hell

https://www.youtube.com/watch?v=8aGhZQkoFbQ

