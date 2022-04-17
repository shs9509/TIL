# 프라미스와 async, await



## 콜백

자바스크립트 호스트 환경이 제공하는 여러 함수를 사용하면 *비동기(asynchronous)* 동작을 스케줄링 할 수 있습니다. 원하는 때에 동작이 시작하도록 할 수 있죠.

`setTimeout`은 스케줄링에 사용되는 가장 대표적인 함수입니다.

호출이 계속 중첩되면서 코드가 깊어지고 있네요. 본문 중간중간 `...`로 표시한 곳에 반복문과 조건문이 있는 코드가 들어가면 관리는 특히나 더 힘들어질 겁니다.

이렇게 깊은 중첩 코드가 만들어내는 패턴은 소위 ‘콜백 지옥(callback hell)’ 혹은 '멸망의 피라미드(pyramid of doom)'라고 불립니다.



## 프라미스

- 프라미스 객체

  ```js
  let promise = new Promise(function(resolve, reject) {
    // executor (제작 코드) 이는 무조건 resolve, reject 둘중 하나를 반환해야합니다.
  });
  ```

  - `resolve(value)` — 일이 성공적으로 끝난 경우 그 결과를 나타내는 `value`와 함께 호출
  - `reject(error)` — 에러 발생 시 에러 객체를 나타내는 `error`와 함께 호출

  프로미스 내부에서는 내부 프로퍼티를 갖습니다.

  - `state` — 처음엔 `"pending"`(보류)이었다 `resolve`가 호출되면 `"fulfilled"`, `reject`가 호출되면 `"rejected"`로 변합니다.
  - `result` — 처음엔 `undefined`이었다 `resolve(value)`가 호출되면 `value`로, `reject(error)`가 호출되면 `error`로 변합니다.

- 프라미스의 결과나 에러는 `.then`, `.catch`, `.finally` 메서드를 통해서 전달 받습니다.

  - `then`

    - 첫 번째 인수는 프라미스가 이행되었을 때 실행되는 함수이고, 여기서 실행 결과를 받습니다.
    - 두 번째 인수는 프라미스가 거부되었을 때 실행되는 함수이고, 여기서 에러를 받습니다.

    ```js
    let promise = new Promise(function(resolve, reject) {
      setTimeout(() => resolve("done!"), 1000);
    });
    
    // resolve 함수는 .then의 첫 번째 함수(인수)를 실행합니다.
    promise.then(
      result => alert(result), // 1초 후 "done!"을 출력
      error => alert(error) // 실행되지 않음
    );
    ```

  - `catch`

    - 에러가 발생한 경우만 다루고 싶은경우 사용합니다.
    - `then(null, errorHandlingFunction)`과 같습니다.

  - `finally`
    - 프라미스가 처리되면 언제나 실행됩니다.
    - 이행됫는지 거부되었는지 상관없기 때문에 인수가 없습니다.
    - 대부분 절차를 마무리하는 동작을 수행하는데 쓰입니다.
    - 이보단 `then(f,f)`를 쓰는게 더 편리합니다.
  - 처리된 프라미스의 핸들러는 즉각 실행됩니다.

## 프라미스 체이닝

프라미스 체이닝을 통해서 비동기처리가 가능합니다.

```js
new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000); 
}).then(function(result) {
  alert(result); // 1
  return result * 2;
}).then(function(result) { 
  alert(result); // 2
  return result * 2;
});
// 화살표 함수를 사용하면 더 편합니다.
new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000); 
}).then(result => {
  alert(result); // 1
  return result * 2;
}).then(result => { 
  alert(result); // 2
  return result * 2;
});
```

`result`가 `.then` 핸들러의 체인을 통해서 전달이 됩니다.

- `.then`에서 프로미스를 생성하거나 반환하는 경우에는 처리될때까지 기다립니다.

  ```js
  new Promise(function(resolve, reject) {
    setTimeout(() => resolve(1), 1000);
  }).then(function(result) {
    alert(result); // 1
    return new Promise((resolve, reject) => { // (*)
      setTimeout(() => resolve(result * 2), 1000);
    });
  }).then(function(result) { // (**)
    alert(result); // 2
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(result * 2), 1000);
    });
  }).then(function(result) {
    alert(result); // 4
  });
  ```

- 핸들러는 프라미스가 아닌 `thenable`이라는 객체를 반환하기도 합니다.

  - `.then`메서드를 가지고 있으면 `thenable`이라고 합니다.

  - 프라미스와 같은 방식으로 처리됩니다.
  - 이는 서드파티 라이브러리가 프라미스와 호환 가능한 객체를 구현하기 위함입니다.



### fetch와 체이닝 응용하기

네트워크 요청시 프라미스를 자주사용합니다.

```js
// user.json에 요청을 보냅니다.
fetch('/article/promise-chaining/user.json')
  // 응답받은 내용을 json으로 불러옵니다.
  .then(response => response.json())
  // GitHub에 요청을 보냅니다.
  .then(user => fetch(`https://api.github.com/users/${user.name}`))
  // 응답받은 내용을 json 형태로 불러옵니다.
  .then(response => response.json())
  // 3초간 아바타 이미지(githubUser.avatar_url)를 보여줍니다.
  .then(githubUser => {
    let img = document.createElement('img');
    img.src = githubUser.avatar_url;
    img.className = "promise-avatar-example";
    document.body.append(img);

    setTimeout(() => img.remove(), 3000); // (*)
  });
```

만약`githubUser`을 하고 나서 이후 행동을 하고 싶다면 프로미스를 반환하여만들어 줍니다.

```js
fetch('/article/promise-chaining/user.json')
  .then(response => response.json())
  .then(user => fetch(`https://api.github.com/users/${user.name}`))
  .then(response => response.json())
  .then(githubUser => new Promise(function(resolve, reject) { // (*)
    let img = document.createElement('img');
    img.src = githubUser.avatar_url;
    img.className = "promise-avatar-example";
    document.body.append(img);

    setTimeout(() => {
      img.remove();
      resolve(githubUser); // (**)
    }, 3000);
  }))
  // 3초 후 동작함
  .then(githubUser => alert(`Finished showing ${githubUser.name}`));
```

- 깔끔하게 재사용 가능한 함수단위로 나눠놓기

  ```js
  function loadJson(url) {
    return fetch(url)
      .then(response => response.json());
  }
  
  function loadGithubUser(name) {
    return fetch(`https://api.github.com/users/${name}`)
      .then(response => response.json());
  }
  
  function showAvatar(githubUser) {
    return new Promise(function(resolve, reject) {
      let img = document.createElement('img');
      img.src = githubUser.avatar_url;
      img.className = "promise-avatar-example";
      document.body.append(img);
  
      setTimeout(() => {
        img.remove();
        resolve(githubUser);
      }, 3000);
    });
  }
  
  // 함수를 이용하여 다시 동일 작업 수행
  loadJson('/article/promise-chaining/user.json')
    .then(user => loadGithubUser(user.name))
    .then(showAvatar)
    .then(githubUser => alert(`Finished showing ${githubUser.name}`));
  ```

  

## 프라미스와 에러핸들링

에러 핸들링은 보통 `catch`를 통해서 에러를 처리합니다.

프라미스에서는 보이지 않는 `try .. catch`가 있습니다. 이는 예외를 잡아주면 `reject`처럼 다룹니다.

- `.catch`는 `.then` 핸들러에서 발생한 모든 에러를 처리할 수 있습니다.

- `.catch`에서  `throw`를 사용하면 가장 가까운 에러 핸들러로 넘어갑니다. 그리고 에러가 성공적으로 처리가되면 가장 가까운 `.then`핸들러로 넘어갑니다.

  ```js
  // 실행 순서: catch -> then
  new Promise((resolve, reject) => {
    throw new Error("에러 발생!");
  }).catch(function(error) {
    alert("에러가 잘 처리되었습니다. 정상적으로 실행이 이어집니다.");
  }).then(() => alert("다음 핸들러가 실행됩니다."));
  ```

- 에러를 처리하지 못하면 전역에러를 생성합니다.

  - 브라우저에서는 이것은 `unhandledrejection` 이벤트로 다룰 수 있습니다.

    ```js
    window.addEventListener('unhandledrejection', function(event) {
      // 이벤트엔 두 개의 특별 프로퍼티가 있습니다.
      alert(event.promise); // [object Promise] - 에러를 생성하는 프라미스
      alert(event.reason); // Error: 에러 발생! - 처리하지 못한 에러 객체
    });
    new Promise(function() {
      throw new Error("에러 발생!");
    }); // 에러 처리 핸들러, catch가 없음
    ```

- 에러가 발생하고 회복할 방법이없다면 `catch`를 사용하지않아도 됩니다.



## 프라미스 API

프라미스 클래스에는 5가지 정적 메서드가 있습니다.

### Promise.all

- 복수의 URL에 동시에 요청을 보내고 콘텐츠를 처리할 때 사용합니다.

- 결과값을 담은 배열이 반환됩니다.

  - 가장 첫번째에있는게 가장 앞에있습니다. 오래걸리더라도!

- 프라미스중 하나라도 거부되면 전체가 거부됩니다.

  - 이행된 프라미스도 잊혀집니다.

  ```js
  let urls = [
    'https://api.github.com/users/iliakan',
    'https://api.github.com/users/remy',
    'https://api.github.com/users/jeresig'
  ];
  // fetch를 사용해 url을 프라미스로 매핑합니다.
  let requests = urls.map(url => fetch(url));
  // Promise.all은 모든 작업이 이행될 때까지 기다립니다.
  Promise.all(requests)
    .then(responses => responses.forEach(
      response => alert(`${response.url}: ${response.status}`)
    ));
  ```

### Promise.allSettled

> 최근에 추가된 문법입니다. 구식브라우저는 폴리필이 필요합니다.

모든 프라미스가 처리될 때까지 기다립니다.

- `promise.all`과 다르게 실패해도 다른 요청결과는 남아있습니다.

  ```js
  let urls = [
    'https://api.github.com/users/iliakan',
    'https://api.github.com/users/remy',
    'https://no-such-url'
  ];
  
  Promise.allSettled(urls.map(url => fetch(url)))
    .then(results => { // (*)
      results.forEach((result, num) => {
        if (result.status == "fulfilled") {
          alert(`${urls[num]}: ${result.value.status}`);
        }
        if (result.status == "rejected") {
          alert(`${urls[num]}: ${result.reason}`);
        }
      });
    });
  ```

### Promise.race

`Promise.all`과 비슷하지만 가장 먼저 처리되느 프라미스의 결과를 반환합니다.

나머지는 프라미스 결과는 무시합니다.

### Promise.resolve/reject

 `async/await` 문법이생긴뒤로 쓸모없어졌습니다.

- `Promise.resolve(value)` – 주어진 값을 사용해 이행 상태의 프라미스를 만듭니다.

- `Promise.reject(error)` – 주어진 에러를 사용해 거부 상태의 프라미스를 만듭니다.



## 프라미스화

콜백을 받는 함수를 **프라미스를 반환하는 함수**로 바꾸는 것을 프라미스화라고 합니다.

이는 콜백을 완전히 대처하지 못합니다. 콜백은 여러번 호출할수 있으나 프라미스는 하나의 결과만 가질 수 있기 때문입니다.

```js
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`${src}를 불러오는 도중에 에러가 발생함`));

  document.head.append(script);
} // 이거를 바꾸면
let loadScriptPromise = function(src) {
  return new Promise((resolve, reject) => {
    loadScript(src, (err, script) => {
      if (err) reject(err)
      else resolve(script);
    });
  })
}
// 사용법:
// loadScriptPromise('path/script.js').then(...)
```

그런데 이것은 `loadScript`에대한 프로미스화일뿐 헬퍼함수로 만들어보자

프라미스를 적용할 함수 `f` 를 받고 레퍼함수를 반환하는 함수 `promisify(f)`를 만듭니다.

```js
function promisify(f) {
  return function (...args) { // 래퍼 함수를 반환함
    //args는 여기서 src	
    return new Promise((resolve, reject) => {
      function callback(err, result) { // f에 사용할 커스텀 콜백
        if (err) {
          reject(err);
        } else {
          resolve(result);
        }
      }
      args.push(callback); // 위에서 만든 커스텀 콜백을 함수 f의 인수 끝에 추가합니다.
      f.call(this, ...args); // 기존 함수를 호출합니다.
    });
  };
};

// 사용법:
let loadScriptPromise = promisify(loadScript);
loadScriptPromise(...).then(...);
```

> 이건 좀 어려운뎀...



## 마이크로테스트



## async 와 await
