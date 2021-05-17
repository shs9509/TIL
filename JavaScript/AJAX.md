let  새로할당	가능

const 새로할당 불가능



블록스코프 안에는 아예다른 구간이라고 생각하고

변수를 쓴다.



호이스팅

변수의 선언을 뒤에서 하는것

var의 경우 호이스팅이 일어남 (undefined가 나타남)



파이썬과 다르게 자바스크립트의 Boolean 타입은 

  첫 단어가 소문자



obj.key, obj[key]

 \- indexOf 메서드를 사용합니다.



map

fliter

foreach

```
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

reduce

```
const result = scores.reduce((acc, score) => {
  acc[score.name] = score.score
  return acc
}, {})
console.log(result)
```

원소에 대해서 함수를 연속으로 행해줌





### AJAX

비동기식 자바스크립과 xml 타입

자바스크립의 일부라 json을 많이씀



페이지에서 일부분만 업데이트하기위해서 XMLHttpRequest 를 쓴다.

XMLHttpRequest는 서버와 상호작용하기위해 쓰고

새로고치없이 URL로 부터 데이터를 가져올수있다.

생성자 = XMLHttpRequest()

```javascript
const request = new XMLHttpRequest() //생성하고
const url = 'http://~~'	// 데이터를 얻어올 url

request.open('GET',url) // 데이터를 준비하고
request.send()	// 요청보내기

const data = request.response// 받은응답
console.log(data) //근데 응답안온채로 출력한거라 아무것도안뜸 (스레드가 한개라)
```

이런식



