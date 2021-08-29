이글은 [ 모던 자바스크립트 핵심 가이드] 의 책을 통해서 배운 내용을 정리한 글입니다.



# :rabbit2: var / let / const

ES6가 되면서 변수정의에 'let' 과  'const' 가 추가되었다.



기존 var의 경우 함수스코프에서 종속되며  for 루프 안에서 선언해도  루프밖에서도 접근가능하다.



let 은

블록스코프에 종속된다. 선언된 부분과 그하위에서만 사용가능



const 는

let 과 마찬가지로 블록스코프에 종속된다.

차이점은 값의 재할당이 불가능하다.

객체 값의 재할당이라면?? 상관없다. 속성을 재할당하는 행위이기 때문

```javascript
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





# :bow_and_arrow:화살표 함수

ES6 가 나오면서 "=>" 를 통해 함수를 선언하는 방법이 생겼다.



기존의 ES5 의 함수선언

```javascript
const multiple = function(a,b){
	return a*b;
}
```



ES6 의 화살표함수 적용

```javascript
const multiple = (a,b) => {
	return a*b;
}

// 더 간단하게?

const multiple = (a,b) => a*b;
```



뭐가 달라졌나면 `function(a,b)` 가 ` (a,b) =>` 으로 표현이 가능해졌다.

그외

- 매개변수가 하나인 경우

```javascript
const num = a =>{
	return `${a} 명 생존`;
}
// () 생략이 가능하다.
```



- 그러면 매개변수가 없으면????

```javascript
const num = () =>{
	return "자바스크립트 어려지않아오";
}
// () 는 무조건 적어줘야한다.
```





### :thinking: 그런데 이것뿐인가??

먼저 `this` 에서 변화가 생긴다. (**중요**)

기존 ES5 함수안에서 `this`를 사용하면 `this`는 해당 함수를 가리킨다.

하지만 화살표함수를 사용할경우 `this`는 상위스코프에 상속이 된다.

// 이는 최근에 프로젝트를 진행하면서도 겪었던 문제였다.

https://medium.com/@hozacho/vuejs%EC%97%90%EC%84%9C-arrow-function%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-ec067c342412



```html
<div class="box open">
    box
</div>
```

```css
.open{
    background-color: red;
}
```

```javascript
const box = document.querySelector(".box");
box.addEventListener("click",function(){
    this.classList.toggle("open");
    setTimeout(function(){
        this.classList.toggle("open");
    }, 500);
});

// 여기서 첫번째 this는 box를 가리키고 두번째 this는 window를 가리킨다.
// 두번째 this 역시 상위 스코프인 box를 가리키려면 =>를 사용하자.

box.addEventListener("click",function(){
    this.classList.toggle("open");
    setTimeout(()=>{
        this.classList.toggle("open");
    }, 500);
});
```



주의해야될점은 상위스코프에 상속이되므로 

상위스코프가 window인 경우에는 의도한게 아니라면 피하도록 하자.



추가적인 차이점으로 arguments 객체에 대한 접근방식이다.

```javascript
function study(){
	consle.log(arguments[0]);
}

study(css, HTML, JavaScripts)
// css
```



`this`처럼 `arguments` 역시 화살표함수를 사용하면 부모스코프의 값을 상속한다.

오히려 값이 안나올수있으니 화살표 ,function 을 구분해서 사용해주자.





# :black_joker: ​기본값 

ES6 에서 기본값을 설정하는데 편의를 개선했다.



```javascript
function mystatus(power=10, dex=10, int=10){
	return power*0.2 + dex*0.8 + int;
}

mystatus(30)
// 24
// 값을 정해주지않으면 기본값으로 설정된다.
```

 

###  :thinking: power 값을 설정 안하고, 나머지를 설정하고 싶으면 어떻게 해야할까?

```javascript
mystatus(undefined,30,30)
// 이렇게 해줘도 되긴한다.
```

조금 더 좋은방식으로 써보자



destructuring 을 사용하자

```javascript
function mystatus({power=10, dex=10, int=10} = {}){
	return power*0.2 + dex*0.8 + int;
}
// 이런식으로 인수를 바꿔주면

mystatus({dex = 30, int = 30});
//이렇게 받을수가있다.

mystatus({});
// 이러면 기본값으로 설정된다. //20
```



![image-20210823023705844](ECMAScript6.assets/image-20210823023705844.png)



`={}` 를 빼고 진행했다. 그런데 왜 `abs({});` 는 되는건지 의문이긴하다. (책에선 안된다고 했음!)





# :seat: 템플릿 리터럴

ES6에서 백틱` `` `을 통한 문자열 삽입이 가능해졌다.

 

```javascript
let name='신형식';
const greeting = `제 이름은 ${name}입니다. 반갑습니다.`;
console.log(greeting);
// "제 이름은 신형식입니다. 반갑습니다."

let a=4;
let b=5;
console.log(`a+b = ${a+b}`)
//a+b = 9

let hi = `안녕하세요
반갑습니다.`
// ``을 통해서 여러줄을 감싸는것도 가능해졌다.
```

이와 연계해서 

삼항연산자나 함수를 넣어서 사용하는등 다양하게 사용할 수 있다.





# :sunflower: 문자열 메서드

문자열에 해당하는 기존 메서드들을 살펴보자

```javascript
const str = "How are you DOING?"
str.indexOf("are");
//4
str.slice(0,5);
//How a
str.touppperCase();
//HOW ARE YOU DOING?
str.toLowerCase();
//how are you doing?
```



새로운 메서드들을 살펴보자

```javascript
const str = "How are you DOING?"
str.starsWith("How");
//true
str.starsWith("How",3);
//false 3개이후를 검사!
str.endsWith("Ing");
//false
str.endsWith("w",3);
//true 첫믄자 3개만 고려!
str.Includes("are");
//true
str.repeat(3);
//"How are you DOING?How are you DOING?How are you DOING?"
```

알아야할것

- 대소문자를 구별한다.



# :dagger:디스트럭처링

디스트럭처리은 배열의 값이나 객체의 속성을 풀어서 별개의 변수로 사용하기 쉽게 만든다.



- 객체 디스트럭처링 `{ }`

```javascript
const person = {
    first:"신형식",
    second:"아람즈",
};
//[기존] 객체에서 변수를 받는다
const first = person.first;
const second = person.second;

//[ES6] 
const {first,second} = person;
const {first: f} = person.frist; // 변수의 이름 변경도 가능하다.
const {first: f = "무명"} = person.frist; // 디폴트값 설정도 가능하다.
console.log(f) // "신형식" 
console.log(first)// 오류 (변경시 기존first는 변수명이아니다.)
```



- 배열 디스트럭처링 `[ ]`

```javascript
const person = ["신형식","27","shs950930@gmail.com"];
const [name,age,email] = person;

// 레스트 연산자를 사용해보자
const [...shin]  = person;
console.log(shin);
// ["신형식","27","shs950930@gmail.com"]
```



- 변수교체

```javascript
let apple = "노랑";
let banana = "빨강";

[apple,banana] = [banana,apple]
//이러면 교체됨
```



# :curly_loop: 루프

ES6 에서는 새로운 유형의 루프인 `for of` 가 도입되었다.



기존의 반복을 위해서는 `for` `for in`  같은 것을 썼다.

`for of` 예시를 통해 다른점을 살펴보자

```javascript
const fruits =["apple", "banana", "mango", "watermelon"];

for(const fruit of fruits){
	console.log(fruit);
}
//apple
//banana
//mango
//watermelon
```

바로 원소에 접근해서 나열이 가능하다.



:thinking: 그럼 객체에 대한 반복은 똑같이 가능할까?

```javascript
const person ={
	name:"신형식",
	age:28,
	email:"shs950930@gmail.com"
};
for(const stat of person){
	console.log(stat);
}

//Uncaught TypeError: person is not iterable
```

안된다.

그러면 필요한것이 `Object.keys()` 입니다.

 이를 통해서 key를 얻고 따로 key 에 맞는 value를 저장해서 출력합니다.

```javascript
const person ={
	name:"신형식",
	age:28,
	email:"shs950930@gmail.com"
};
for(const stat of Object.keys(person)){
	const value = stat;
    console.log(value ,person[value]);
}

```



# :goal_net:배열 메서드

ES6 에서 배열 메서드가 다수 도입되었다.



- Array.from()
  - 배열이 아닌것을 받아서 배열로 변환해서 반환해준다.
- Array.of()
  - 전달받은 인수를 배열로 생성한다.
- Array.find()
  - 조건에 충족되는 첫번째 원소를 반환한다.
- Array.findIndex()
  - 조건에 충족되는 첫번째 원소의 인덱스를 반환한다.
- Array.some()
  - 조건에 충족되는게 있는지 확인한다.
- Array.every()
  - 조건에 모든원소가 충족되는지 확인한다.



# :red_car:스프레드 연산자와 레스트 매개변수

`...` 이 스프레드 문법이다



**배열의 결합**이 가능하다.

```javascript
const code = ["java","c++","c","python"];
const front = ["CSS", "HTML", "Javascripts"];
const develop = [...code, "Spring", ...front];
console.log(develop);
//["java", "c++", "c", "python", "Spring", "CSS", "HTML", "Javascripts"]
```



**배열의 복사**에도 용이하다.

```javascript
const code = ["java","c++","c","python"];
const c_code = [...code];
```

기존의 ES5에서는 `concat`을 사용해서 복사를 했어야되었다.

```java
const code = ["java","c++","c","python"];
const c_code = [].concat(code);
```



스프레드를 통해서 손쉽게 값을 넣을 수 있다.

```javascript
function multiple(a,b){
    return a*b;
}

const one = [4,6];
const value = multiple(...one);
console.log(value)
//24
```



**ES2018에서는 객체에도 스프레드 연산자가 적용이된다!**



`...` 이것은 레스트 문법이다. 

:thinking:??????



생긴것은 같지만 스프레드가 '**확장**'을 맡는다면 레스트는'**축소**'를 맡는다.

```javascript
const parts=["글카","SSD","모니터"];
const [...computer] = parts;
console.log(computer);
//["글카", "SSD", "모니터"]
```





# :robot:객체 리터럴의 업그레이드

ES6 가되어서 객체 리터럴 표기법이 다양하게 개선되었다.



```javascript
const name="신형식";
const age=27;
const sex="male";
const job="frontend developer";

// 이를 객체로만들고 싶다면
const me ={
    name,
    age,
    sex,
    job,
    greet(){
        console.log("good");
    },
}
console.log(me)
//{name: "신형식", age: 27, sex: "male", job: "frontend developer"}
```

깔끔하다!  ES5 라면 `name`, `age` 일일히 값까지 적어 줘야했을 것이다.

함수역시 `function` 을 적어주지 않아도 된다.



객체의 속성을 동적으로 정의할때 간소화되었다.

```javascript
//ES5
var name="신형식";
var person ={};
person[name]="신형식"

// 빈 객체를 만들어놓고 채워줘야하는 번거로움!

//ES6
const name = "신형식";
const person = {
    [name] = "신형식"
}
//생성하면서 바로 할당이 가능하다.
```





# :symbols:심볼

ES6에서는 심벌이라는 새로운 원시자료형이 추가되었다.



심볼은 항상 고유하다!!!!!

```javascript
const my_apple = Symbol('json');
console.log(my_apple);
//Symbol(json)
```

이런식으로 나타나기는 하는데...

고유한 성질을 어떤 상황에서 쓰이는건가?

```javascript
const my_apple = Symbol('json');

const your_apple = Symbol('json');

console.log(my_apple == your_apple);
console.log(my_apple === your_apple);
//false
//false
```

분명 같은 값으로 했음에도 불구하고 다른값으로 인식이된다.

직책이나 직급같은경우 같은이름이 많기 때문에 이를 인식 해주려면 쓰는것이 편하다.

하지만 `for in` 을 통한열거는 불가능하다.

속성의 배열을 얻기위해서는 `Object.getOwnPropertySymbols()`를 사용하자.

```javascript
const office = {
    [Symbol("Tom")]:"CEO",
    [Symbol("Json")]:"CTO",
    [Symbol("Json")]:"CIO"
}

const symbols = Object.getOwnPropertySymbols(office);
console.log(symbols);
//[Symbol(Tom), Symbol(Json), Symbol(Json)]

const value = symbols.map(symbol => office[symbol]);
console.log(value);
//["CEO", "CTO", "CIO"]
```





# :classical_building: 클래스



클래스 생성

```javascript
class Person{
  // 클래스 선언 
}

const me = class Person{
    // 클래스 표현식
}
// 클래스 선언과 표현은 호이스팅되지않는다 꼭 선언 먼저 하자.
```



```javascript
class Person{
    constructor(name,age){
        this.name = name;
        this.age = age;
    }
    greet(){
        console.log(`안녕 내이름은 ${this.name} 이고 나이는 ${this.age}야`);
    }
    farewell(){
        console.log("잘잇으라구");
    }
    static info(){
        console.log("가나다라마바사")
    }
}

const shin = new Person("신형식",27);
shin.greet();
//안녕 내이름은 신형식 이고 나이는 27야
shin.farewell();
//잘잇으라구

shin.info();
// 에러!!!!
Person.info();
//가나다라마바사
```

​	**정적메서드는 인스턴스에서 접근이 불가능하다.**



`get` 과 `set`을 통해서 값을 불러오거나 설정할 수 있다.

```javascript
class Person{
    constructor(name,age){
        this.name = name;
        this.age = age;
        this.nickname = "";
    }
    set nicknames(value){
        this.nickname = value;
        console.log(`${this.nickname}`);
    }
    get nicknames(){
        console.log(`현재 제 별명은 ${this.nickname}`);
    }
}

const shin = new Person("신형식",27);
shin.nicknames="짱구아빠";
//짱구아빠
shin.nicknames;
//현재 제 별명은 짱구아빠
```



기존클래스를 상속한 새로운 클래스를 쓰려면 `extents`를 사용한다.

```javascript
class Adult extends Person{
	constructor(name,age,work){
        super(name,age);
		this.work = work;
	}
}
const dad = new Adult("신형만",45,"개발자")
```



배열의 확장

```javascript
class Classroom extends Array {
    constructor(name, ...students){
        super(...students);
        this.name = name;
    }
    add(student){
        this.push(student);
    }
}
const myClass = new Classroom("1A",
                              {name:"Tim",mark:6},
                              {name:"dfim",mark:5},
                              {name:"Tifgm",mark:3},
                              {name:"erwim",mark:2},
                             );
myClass.add({name:"Timmy", mark:7});
myClass[4];
//{name: "Timmy", mark: 7}
```







