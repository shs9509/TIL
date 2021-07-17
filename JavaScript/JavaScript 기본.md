# JavaScript 기본



웹문서의 각요소를 가져와서 필요에따라 스타일을 변경하거나 움직이게 할수있다.



- 웹의 요소를 제어
- 웹 애플리케이션을 제작

- 다양한라이브러리 사용가능
- 서버개발 가능 (Node.js)



------------

:first_quarter_moon: **웹 애플리케이션? 웹사이트?**

- **웹 애플리케이션** : 웹브라우저와 웹기술을 사용하여 사용자와 대화하는 대화식으로 인터넷을 사용하는 컴퓨터 프로그램

  ex) 요즘 댓글도 달수있고 검색도 할수있는 블로그나 사이트들

  

- **웹 사이트** : 웹페이지의 모음 

  ex) 그냥 볼수만 있는 뉴스페이지나 블로그

------------



주의 

대소문자 구별한다.



외부 자바스크립트파일 연결

```html
<script src="외부 스크립트 파일경로"></script>
```



자바스크립트의 구조

식 , 문



기본적인 기능

```html
<script>
    alert('경고!');
	var reply =confirm("확인을 누를 껀가요?");
   	var id = prompt("id를 입력해주세요","shs9509");
	var id = prompt("id를 입력해주세요");
    document.write("<h1> 제목 </h1>");
</script>
```

응용

```html
<script>
	var id = prompt("id를 입력해주세요");
	document.write("안녕"+id+"!");
    console.log("안녕"+id+"!");
</script>
```

+console.log()

콘솔창에 괄호안을 표현해준다. 이를 통해 오류나 변수값을 확인한다.



- 스타일 가이드

  - 구글이나 에어비엔비 참고

  - 식별자

    ```html
    num1; //첫글자는 영어와 '_'
    _takeTime(); // '_' 로 시작가능 , 두단어가 합쳐질시 카멜케이스 사용
    onTime();
    ```



- 변수선언, 할당

  ```js
  var 변수명
  var apple;
  var banana, melon, ju;
  banana = 2500;
  
  var goal = 2004;
  ```



- 조건식

  ```js
  if(조건){  }else{  }
  
  
  (조건) ? true인 경우 | flase인 경우
  
  
  switch(조건)
  {
      case 값1 : 명령
      	break
      case 값2 : 명령
      	break
      case 값3 : 명령
      	break
      default: 명령
  }
  ```

  

- for 문

  ```js
  for ( 초기값; 조건; 증가식){
      명령
  }
  
  for( i=1 ; i<10 ; i++){
      sum +=i
  }
  ```

  

- while문

  ```js
  while(조건){ 실행 }
  do{ 실행 }(조건)
  ```

  

-------------



함수



```js
function addNumber(num1, num2){
    var sum = num1 + num2;
    alert(sum);
}
document.write(addNumber(2,3));
```



변수가 적용되는 범위 '스코프(scope)'

한 함수에만 쓰이는 것은 지역변수, 로컬변수

스크립트 전체에서 사용할수있는 변수 전역변수, 글로벌 변수

var로 선언한변수는 함수안에서만 쓰인다.

전역변수를 쓰려면? 함수밖에서 선언하거나 , var를 쓰지않는다.



호이스팅(hoisting)

var를 쓰면은 var를 쓴변수를 먼저 파악하고 값은 나중에 파악한다.

그결과 출력뒤에 값이 정해진다면 변수는 존재하나 값을 나타낼수없는 undefined로 나타나진다.



var는 재선언 재할달이 가능하다.



let const

ES6가 나오면서 var를 대체하기위해 생긴 예약어 

가장큰차이는 스코프범위

var 은 함수영역의 스코프

let const 는 블록영역( { } )의 스코프

```js
function calcSum(n) { // sum은 여길 못벗어남
      let sum = 0;
      for(let i = 1; i < n + 1; i++) {	//i는 여길 못벗어남					
        sum += i;	
      }      
      console.log(sum);
    }    
    calcSum(10); 
```

전역변수는 여전히 예약어를 안쓰면 된다.

let은 재할당은 되지만 재선언은되지않는다. (그러니 흔히 쓰이지않는 유니크한 단어인거임)

let 호이스팅이없다. 변수값을 설정해야지 쓸수있다고 경고가 뜬다.



const  상수값이라는뜻 변하지않는다!!

즉, 재선언과 재할당을 할수없다.



- 변수 사용법
  - 전역변수는 최소한으로 사용한다.
  - var변수는 함수에서 우선적으로 선언한다. (호이스팅떄문)
  - for 문 안에서 var 변수를 쓰지말자 왜냐면 어차피 함수레벨 스코프이기 떄문
  - ES6 라면 var 보다 let 을 쓰자



- 함수

  ```js
  function multiple(a,b=5,c=10){
     sum = a*b*c
     return sum
  }
  ```



- 익명함수

  함수에 이름이없음! 매개변수를 이용한다.

  ```js
  var multiple = function(a,b){
      return a*b;
  }
  document.write(mutiple(4,5));
  ```

  

- 즉시실행함수

  선언하면서 실행해버리기

  ```js
  (function(){
      document.write("안녕못해요 저리가버리세요.");
  }());
  
  (function addNumber(a,b){
      sum = a+b;
  }(3,4));
  document.write(sum);
  ```

  

  익명함수만 매개변수에 따라 달라짐

  ES6 가 되면서 화살표(=>)를 통해서 더욱 간단하게 표현가능하다.

  매개변수 없는경우

  ```js
  //매개변수 없는경우
  const hi = function(){
      return "안녕!";
  }
  
  const hi = () =>{
  	return "안녕"!;
  }
  
  const hi =()=> "안녕!";
  
  //매개변수 한개인 경우
  let hi = function(user){
      document.write(user+"안녕!");
  }
  
  let hi = user => {document.write(user+"안녕!");}
  
  //매개변수 2개 이상
  let hi = function(oppnent, me){
      document.write( me + "안녕!" + oppnent);
  }
  
  let hi = (oppnent,me) => {document.write( me + "안녕!" + oppnent);}
  ```

  ```js
  매개변수 = 인수 => 명령문 (return 이면 그대로 넣기)
  ```



- 이벤트

  이벤트가 일어나면 이를 처리해주는 함수 -> 이벤트 핸들러

  - 기본

    ```js
    <태그 on이벤트명 ="함수명">
    <button onclick="alert('클릭함!')"> 버튼 </button>
    ```

  - DOM을 이용한 이벤트 처리기

    HTML 의 요소를 가지고와서 이벤트 처리기를 연결할수있다.

    ```js
    웹요소.onclick =함수;
    ```

    ```html
    <button id='chage'>버튼</button>
    <p>lorem</p>
    
    # 1
    var changeButton = document.queryselector(#change);
    changButton.onclick = changeColor 
    
    function changeColor(){
    	doucument.queryselector("p").style.color = "#f00";
    }
    
    # 2
    document.queryselector(#chage).onclick = changeColor;
    
    
    # 3
    document.queryselector(#chage).onclick = function(){
    	doucument.queryselector("p").style.color = "#f00";
    }
    
    ```

    

----------------



## :package: 객체

프로그램에서 인식할수있는 모든대상

자바스크립트에서 객체는 참조형태로 사용 -> 인스턴스의 형태로 사용

객체를 기반으로 해서 인스턴스를 계속 만들어내는 것 + 식별자를 붙여서 사용



인스턴스 만들기

new  객체명

```js
var now = new Date();
document.write(now);
```



객체에는 프로퍼티 , 메서드가있음

프로퍼티

​	객체의 특징이나 속성을 나타냄

메서드

​	객체에서 할수있는 동작

이것들 역시 인스턴스로 바꿔주자

'.' 붙이고 그대로 쓰면됨

```js
var now = new Date();
document.write(now.toLocaleString());
```



- Array 객체

  만들기

  ```js
  var li = new Array();
  var li = new Array(4); // 크기
  var li = ["1","2","3","4"];
  var li = Array("1","2","3","4");
  
  li.length // 길이
  ```

  참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array



































