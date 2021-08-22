참고[ 모던 자바스크립트 핵심 가이드]



# :rabbit2: var / let / const

ES6가 되면서 변수정의에 'let' 과  'const' 가 추가되었다.



기존 var의 경우 함수스코프에서 종속되며  for 루프 안에서 선언해도  루프밖에서도 접근가능하다.



let 은

블록스코프에 종속된다. 선언된 부분과 그하위에서만 사용가능



const 는

let 과 마찬가지로 블록스코프에 종속된다.

차이점은 값의 재할당이 불가능하다.

객체 값의 재할당이라면?? 상관없다. 속성을 재할당하는 행위이기 때문

```
const energy = {
	speed:2.5,
	power:40,
}
energy.speed =3;
console.log(energy.speed);
// 3

Object.freeze(energy); 
// 이것을 통해 속성값 역시 불변하게 만들수있다.
```



var /  let,const 의 대표적인 차이가 있다면 TDZ에 영향을 받는가 이다.

TDZ 는 어휘적 바인딩이 실행되기 전까지 액세스할 수 없는 현상이다.



그 결과로 

var의 경우 정의되기전 접근이 가능하다! (undefined 지만..)

하지만 let, const 의 경우 에러가 떠버린다.  정의를 꼭 먼저해야하는 것! :man_judge:



이러한 과정이 Hoisting 이라는 개념과 관련이 많다.

> Hoisting 이란

> 스코프 안의 어디에서든 변수 선언은 최상위에서 선언된 것과 동등하게하는 것이다.

즉 var 는 Hoisting이 가능한것이다.

그런데 그럼  let, const는 불가능한걸까? 결론적으로 가능하지만 의미는없다.

 let, const은 선언되기전 TDZ 에 있기때문에 이를 접근하려고하니 에러가 생기는 것이기 때문이다.



 

정리

```
1. 변수정의에는 const, let 있다.
2. 재할당이 필요한 경우 let 그외엔 const를 쓰자 
3. ES6 에서 var는 쓰지않는다.
```



