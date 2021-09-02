# Vue.js 멀티파트, 파일 업로드



## :thinking: 생각하기

블로그나 게시글을 작성할때 파일을 업로드기능은 기본적인 요소이다. 

이미지라던가, 영상이라던가, zip 파일이던가.... 이들을 같이 올림으로서 게시글의 퀄리티가 훨씬 올라간다.



보통 이미지를 업로드한다고 생각했을때 어떤 방식으로 되있는가?

1. 파일 업로드 버튼 클릭

2. 사진들을 고른다.

3. 업로드 될 사진들을 보여준다.

4. 그 사진들을 드래그하거나 게시글 사이에 삽입을 통해 게시글에 같이 배치를 한다.

5. 게시하게 되면 게시글과 함께 사진들이 올라간다.



사진들을 드래그해서 게시들 사이에 배치시키는 것은 생각보다 어려움이 있을 것이다. 

또한 내가 구현하는 SNS 프로젝트에서는 그러한 기능까지 요구하지 않는다.

그래서 4의 진행과정은 생략하려고 한다. ( SNS는 사진과 짧은 글이 대부분이기 때문이다.)



 

## :e-mail: 멀티파트 ?

파일을 업로드 하기 위해서는 멀티파트에 대해서 알아야한다.



모든 텍스트, 이미지, 파일들은 **바이너리(0,1)** 로 이루어져 있다.

그런데 이 상태로 전송은 **불가능**하다! 

전송시에는 **아스키 코드**로서 바꿔야만 가능하다.

그래서 데이터를 **MIME 타입**으로 변환 후 전송을 한다. 



MDN에 따르면

> **MIME 타입**이란 클라이언트에게 전송된 문서의 다양성을 알려주기 위한 메커니즘입니다: 웹에서 파일의 확장자는 별  의미가 없습니다. 그러므로, 각 문서와 함께 올바른 MIME 타입을 전송하도록, 서버가 정확히 설정하는 것이 중요합니다. 브라우저들은 리소스를 내려받았을 때 해야 할 기본 동작이 무엇인지를 결정하기 위해 대게 MIME 타입을 사용합니다



MIME TYPE 에는

텍스트, 이미지, 오디오, 비디오, 모든 이진데이터 등 **개별타입**과 더불어서

MIME TYPE 들이 묶여진 **멀티파트 타입** 으로 된다.



게시글을 올릴시 

**게시글내용, 이미지등 다양한 데이터**가 넘어가므로 이는 **멀티파트 타입**에 해당되게 됩니다.



- `multipart/form-data`은 브라우저에서 서버로 [HTML Form](https://developer.mozilla.org/en-US/docs/Learn/Forms)의 내용을 전송 시 사용할 수 있습니다.

  :tada: 예시코드

  ```html
  <form action="http://localhost:8000/" method="post" enctype="multipart/form-data">
    <input type="text" name="myTextField">
    <input type="checkbox" name="myCheckBox">Check</input>
    <input type="file" name="myFile">
    <button>Send the file</button>
  </form>
  ```

  

  

https://www.bottlehs.com/vue/vue-js-%ED%8C%8C%EC%9D%BC%EC%97%85%EB%A1%9C%EB%93%9C/

이분의 글은 매번 유용하게 쓰는듯합니다. 원리와 개념을 잘 적으셔서 베이스를 잘 쌓는거 같지만.,, 너무 어렵습니다..ㅠㅠ

https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types

+MDN



## :hear_no_evil: 그럼 form 데이터 전송은 어떻게?



폼데이터 ?

https://developer.mozilla.org/ko/docs/Web/API/FormData

> 인코딩 타입이 `"multipart/form-data"`로 설정된 경우, form에서 사용하는 것과 동일한 포맷을 사용해야 합니다.



```html
<form action="http://localhost:8000/" method="post" enctype = "multipart/form-data">
	<input id="file" type="file" accept="image/*" multiple>
</form>

```

- `enctype = "multipart/form-data"` 은 필수적으로 적용해야한다. 
-  `method="post"` 역시 적용하기도 하나 axios에서 post로 지정했기떄문에 

```javascript
import axios from 'axios'
  export default {
    name:'Create',
    data(){
      return{
        content:"",
        afiles:File,
      }
    },
    methods:{
    articleCreate(){
      const formData = new FormData();
      formData.append("content", this.content);
      formData.append("files", this.afiles);
      axios({
        url:'http://127.0.0.1:8080/article',
        method:'post',
        headers: {
          'x-auth-token': `${localStorage.getItem('token')}`,
          'Content-Type': 'multipart/form-data'
        },
        data:formData,
      })
        .then(res=>{
          this.$router.push({ name:'Main'})
        })
        .catch(err=>{
          console.log(err)
        })
      },
    }
  }
```





------------

멀티파트 , 폼데이터

https://velog.io/@sa833591/form-data-%EA%B7%B8%EB%A6%AC%EA%B3%A0-MultipartFile

멀티파드 전송

https://codingnotes.tistory.com/73

Spring 폼데이터 전송

https://velog.io/@pyo-sh/Spring-Boot-%ED%8C%8C%EC%9D%BC%EC%9D%B4%EB%AF%B8%EC%A7%80-%EC%97%85%EB%A1%9C%EB%93%9C-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0

axios 사용시 폼데이터 전송

https://doogle.link/axios-%EC%82%AC%EC%9A%A9%EC%8B%9C-%ED%8F%BC-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%86%A1%ED%95%98%EA%B8%B0-%ED%8C%8C%EC%9D%BC-%EC%97%85%EB%A1%9C%EB%93%9C/

오류와의 싸움

https://stackoverflow.com/questions/68592658/although-i-wrote-enctype-multipart-form-data-error-current-request-is-not-a