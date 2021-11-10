# CSS 적용

페이지 구현하는 유투브

https://www.youtube.com/watch?v=1wfeqDyMUx4





![image-20211011115704798](CSS적용.assets/image-20211011115704798.png)

이렇게하면 해당 버튼에 호버를 하면 색칠이되고, active 가됨



![image-20211011115825493](CSS적용.assets/image-20211011115825493.png)

모든이미지가 통째로 한곳에 모이게됨

물론 section 은 relative임



![image-20211011182104626](CSS적용.assets/image-20211011182104626.png)

경계를 없애줌





![image-20211011182231568](CSS적용.assets/image-20211011182231568.png)

진짜~~~~~ ~~~간단함!!! 





![image-20211011194012561](CSS적용.assets/image-20211011194012561.png)

스크롤에 따른 이동 구현하기



**CSS)**

div { outline: 1px solid red; }

\#container { width: 200px; height: 30px; }

\#cube { width: 30px; height: 100%; background-color: red; }

\#cube:hover { width: 30px; height: 100%; background-color: blue; }



**마크업)**

<div id="container">

  <div id="cube">  </div>

</div>





cube(A)와 container(B) 라는 각각의 요소가 있다고 할 때..

만약 **엘리먼트**A(cube)**가 B영역**(container) 안 바로 다음에 있을 때

**#container:hover > #cube { background-color: yellow; }**

//container(즉 A)라는 아이디를 가진 엘리먼트에 마우스를 호버시키면 cube(즉 B)에 적용된 CSS가 실행된다.



If cube is next to (after containers closing tag) the container: 만약 A가 B영역 밖에 있을 때

**#container:hover + #cube { background-color: yellow; }**



If the cube is somewhere inside the container: 만약 A가 B 영역 안의 어딘가 있을 때

**#container:hover #cube { background-color: yellow; }** 

//hover # 사이에 공란, 즉 스페이스로 칸을 비운댜.



If the cube is a sibling of the container: 만약 A가 B의 자손일 때

**#container:hover ~ #cube { background-color: yellow; }**
