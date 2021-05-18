![image-20210504132144403](C:\Users\ssej0\AppData\Roaming\Typora\typora-user-images\image-20210504132144403.png)



![image-20210504153010647](C:\Users\ssej0\AppData\Roaming\Typora\typora-user-images\image-20210504153010647.png)



자바스크립트



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