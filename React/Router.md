# 라우터

> react-router-dom v6의 문법입니다.

페이지 이동을 리액트 라우터로 처리가 가능하다.



라우터에 컴포넌트가 여러개가 있다.

- `BrowserRouter`: HTML5를 지원하는 브라우저 주소를 감지한다. 이를 사용해 라우트를 크게 감싼다.
- `HashRouter`: 해시 주소를 감지한다.



--------



- 설치 

  ```bash
  npm install react-router-dom
  ```



--------



- `Routes`: 여러 `Route`를 감싸서 규칙이 일치하는 라우트를 렌더링 시켜준다.

- `Route`: `path` 속성에 경로, `element`속성에 컴포넌트를 넣어준다.

  - `*`를 사용해서 여러개의 라우팅을 매칭해줄수있다.

  - ```react
    <Route path="/main/*" element={<Main/>}></Route>
    <Route path="*" element={<NotFound/>}></Route>
    ```

- `Link`: `a`태그를 사용시 페이지를 새로 불러온다. 

  - HistoryApi를 통해서 브라우저 주소 경로만 바꾼다.

  - ```react
    <Link to="경로">링크명</Link>
    ```



-------



- `useParams()`

  `path`에는 `:`를 사용하여 파라미터를 넣을 수 있습니다.

  - 받는 페이지에서는 `useParams()`통해서 받습니다.

  - ```react
    <Route path="/main/:userId" element={<Main/>}></Route>
    ////
    const {userId} = useParams();
    ```



- `useLocation()`
  - hash : 주소의 #문자열 뒤의 값
  - pathname : 현재 주소 경로
  - search : ?를 포함한 쿼리스트링
  - state : 페이지로 이동시 임의로 넣을 수 있는 상태 값
  - key : location 객체의 고유 값, 초기값은 default, 페이지가 변경될 때 마다 고유의 값이 생성된다.



- `useNavigate()` : `Link`컴포넌트를 사용하지 않고 다른페이지를 이동하는 경우

  - 뒤로가기 등에 쓰입니다.

  - ```react
    import React from 'react';
    import { useNavigate } from 'react-router-dom';
    
    const Product = () => { 
        const navigate = useNavigate(); 
        return ( 
            <> 
            <h3>{productId}번 상품 페이지 입니다.</h3> 
            	<ul> 
                	<li><button onClick={() => navigate(-1)}>Go 1 pages back</button></li> 
               		<li><button onClick={() => navigate('/')}>Go Root</button></li>
                	<li><button onClick={() => navigate('/', {replace: true})}>Go Root</button></li>
            	</ul> 
            </> ); 
    } 
    
    export default Product;
    ```

  - `replace`옵션은 기록을 남기지 않습니다.



> https://goddaehee.tistory.com/305



--------

V5 에서 V6로 바뀌면서 

- `Switch`는 `Routes`가 됬습니다.
- `exact`는 사용하지 않습니다.
- `component`는 `element`가 됬습니다.







## 중첩 라우팅

> https://www.daleseo.com/react-router-nested/



