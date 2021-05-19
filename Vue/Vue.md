# Vue.js

접근성, 유연성, 고성능



MVVM 패턴

Model - View - ViewModel

Model	순수 자바스크립

View	웹페이지의 DOM

ViewModel	Vue

Vue가 모델과 view를 양방향 통신함



- Vue instance

  ```vue
  <script>
  	new Vue({
          el: '#app',
          data:{
          messge: '데이터의 속성'
      }
      })
  </script>
  ```

  el

  data

  template

  methods

  created