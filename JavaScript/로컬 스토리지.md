# 로컬 스토리지



페이지에 props를 통해서 데이터를 넘겨주다보면은 해당 페이지를 새로고침시

 props의 데이터가 사라져서 오류가 나타나는 것을 확인할수있다.



그래서 props를 통해서 데이터를 넘기는 것이아닌 로컬스토리지에 저장함으로써 새로고침에도 예방을 할수있도록한다.



리액트나 뷰같은경우 상태관리를 통해서 할수있겠지만 이방법이 간단하다는 점에서 편하다.

```js
// 키에 데이터 쓰기
localStorage.setItem("key", value);

// 키로 부터 데이터 읽기
localStorage.getItem("key");

// 키의 데이터 삭제
localStorage.removeItem("key");

// 모든 키의 데이터 삭제
localStorage.clear();

// 저장된 키/값 쌍의 개수
localStorage.length;
```



주의해야할점은 저장시 오직 문자형태로 지원이된다는 점이다.

숫자를 저장했다고 생각하면 오히려 문자의 형태로 받을것이다.



하지만 그래도 방법을 존재한다.

JSON 형태를 통해서 데이터를 사용하는것이다.

```js
localStorage.setItem('json', JSON.stringify({a: 1, b: 2}))
//undefined
JSON.parse(localStorage.getItem('json'))
//{a: 1, b: 2}
```

위에는 객체의 형태지만 배열역시 가능하다.



로컬스토리지에 저장된 데이터는 웹페이지를 닫음으로서 삭제되지않는다.

그러므로 직접 삭제 해줄수있도록 하자.

```js
localStorage.length
//5
localStorage.key(0)
//"email"
localStorage.removeItem('obj')
//undefined
localStorage.length
//4
localStorage.clear()
//undefined
localStorage.length
//0
```



참조

> https://www.daleseo.com/js-web-storage/

