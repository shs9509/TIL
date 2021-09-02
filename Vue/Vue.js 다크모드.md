# 다크모드

프로젝트의 한기능으로서 다크모드를 구현했다.



<img src="Vue.js 다크모드.assets/image-20210816223619270.png" alt="image-20210816223619270" style="zoom: 33%;" />

<img src="Vue.js 다크모드.assets/image-20210816223611198.png" alt="image-20210816223611198" style="zoom:33%;" />



윈도우의 다크모드에 접근해서 사용하는 방식

색의 대비는 회색과 밝은 금색을 이용했다.

이경우 힘든점은 컴포넌트의 색을 전역으로 관리를 해야 진행하기가 편하다.

또한 다양한 색을 쓸수록 해야할일을 배로 늘어남으로 최적화가 잘되있는것이 좋다.

```css
:root.lightmode {
  background-color: #ffffff;
  /*variables*/
  --background-color:#ffffff;
  --text-color:#181c40;
  --title-color: #42b983;
  --content-color: #777;
  --icon-color:#181c40;
  --dropdown-color:#ffffff;
  --dropdown-text-color:#ffffff;
  --sub-button-color:#2FA8FF;
  --sub-text-color:#ffffff;
  
}

:root.darkmode {
  background-color: #5A5F62;
  /*variables*/
  --background-color:#5A5F62;
  --text-color:#ffffff;
  --title-color: #fafafa;
  --content-color: #6a6e9e;
  --icon-color:#FFF5C3;
  --dropdown-color:#373840;
  --dropdown-text-color:#B1B1B1;
  --sub-button-color:#FFF5C3;
  --sub-text-color:#ffffff;
}
```

이런식으로 항목마다 다크모드 라이트모드를 설정해서 색을 정해놓는다.

이접근방식을 보면서 좀더 효율적으로 할수있었음을 깨달아 버렸다.



로고를 사진을 넣었는데 보시다시피 흰바탕화면이 눈에뜨인다. 이를 위해 svg 나 배경없는 png를 구해야하는 상황이 생겼다.



-------

참고: 

https://velog.io/@katanazero86/%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80-%EB%8B%A4%ED%81%AC-%EB%AA%A8%EB%93%9Cdark-mode-dark-theme-%EC%A0%81%EC%9A%A9

http://icunow.co.kr/guide-darkmode/