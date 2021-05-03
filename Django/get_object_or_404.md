# get_object_or_404



## 0. 404 란?



| 코드 | 메세지    | 설명                                                         |
| ---- | --------- | ------------------------------------------------------------ |
| 404  | Not Found | 문서를 찾을 수 없음. 서버가 요청한 파일이나 스크립트를 찾지 못함 |



![image-20210402163008682](get_object_or_404.assets/image-20210402163008682.png)

이런 상황이 404에러 이다.



## 1. get_object_or_404



기존 페이지에서 벗어나게 되면 페이지 자체가 활동하지 않는 경우가있다.

이경우를 막기위해서 404에러를 나타내게 함으로서 유저에게 알리는것!



get_object_or_404() 의 인자로는 django의 모델을 첫번쨰 인자로 받고, 몇개의 키워드들을 get()에 넘긴다.

객체가 없으면은 HTTP404 에러가 뜬다.