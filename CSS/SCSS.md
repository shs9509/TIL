# SCSS

https://heropy.blog/2018/01/31/sass/

https://yunzema.tistory.com/269



# CSS Preprocessor 란?


CSS 전(예비)처리기, 보통 CSS Preprocessor 라고 부릅니다.

CSS가 동작하기 전에 사용하는 기능으로,

웹에서는 분명 CSS가 동작하지만 우리는 CSS의 불편함을 이런 확장 기능으로 상쇄할 수 있습니다.



Sass는 CSS의 단점을 보정하기 위한 **CSS의 확장**으로 나온 **스크립트 언어**이다.

프로젝트가 점점 커지고, 복잡해져가면서 스타일시트도 덩달아 커지고 관리할게 많아지며 복잡해진다. 이에 따라 유지보수도 당연히 힘들어진다.

이 단점들을 보완하기 위해 **variable, nesting, mixin, inheritance 등**의 개념이 추가된 것이 Sass이다. 

(CSS의 확장)



Sass는 Preprocessing 과정을 통해 css로 해석 및 컴파일 된다.



### **실제 Sass가 가지고 있는 의미**

Sass는 '전처리기(Pre-Processor)'와 그 '구문(Syntax)' 두가지를 모두 지칭한다. 그래서 좀 혼동이 오기도 한다.

Sass는 CSS의 { } 블록이 아닌 들여쓰기 감지를 핵심특성으로 갖는 구문을 가리켰으나, '**Sassy CSS**'를 의미하는 SCSS라는 CSS친화적인 구문을 제공함으로써 Sass와 CSS 사이의 차이를 좁히는 방향으로 변화되어 왔다.

"유효한 CSS라면, 유효한 SCSS이다."

그 이후 Sass(전처리기)는 들여쓰기 구문인 Sass 와 앞서 말한 SCSS의 구문을 모두 사용 가능하며, 동등한 기능을 갖고 있어 원하는 구문을 사용하면 된다. 개취존중.

아무래도 CSS의 구문 형태가 더 익숙하기 때문에 SCSS를 더 많이 선호하는 경향이 있는 듯 하다.

여기서 그러면 SCSS까지 설명이 되었다.



### 어떻게 사용하나요?

위에서 언급한 것처럼 웹에서는 CSS만 동작합니다.
[Sass](https://sass-lang.com/), [Less](http://lesscss.org/), [Stylus](http://stylus-lang.com/) 같은 전처리기(이하 ‘전처리기’로 표기)는 직접 동작시킬 수 없습니다.

우선 전처리기로 작성(코딩)합니다.

전처리기는 CSS 문법과 굉장히 유사하지만 선택자의 중첩(Nesting)이나 조건문, 반복문, 다양한 단위(Unit)의 연산 등… 표준 CSS 보다 훨씬 많은 기능을 사용해서 편리하게 작성할 수 있습니다.

단, 웹에서는 직접 동작하지 않으니 이렇게 작성한 전처리기를 웹에서 동작 가능한 표준의 CSS로 컴파일(Compile)합니다.

전처리기로 작성하고 CSS로 컴파일해서 동작시키는 식



### 왜 Sass(SCSS)죠?

보통 언급되는 전처리기 3대장으로 Less, Sass(SCSS), Stylus가 있습니다.

저는 가장 많이 사용하고 진입장벽이 비교적 낮았던 Less를 처음 사용했습니다.
기본적인 기능은 전처리기들이 다 비슷합니다만 개인적으로 Less는 몇몇 기능에 큰 아쉬움이 있었습니다.
정확하게 언급하진 않겠지만 프로젝트 진행 중 Less에서 제공하는 기능의 한계로 막히는 경우가 몇 번 있었는데 그 기능이 Sass나 Stylus에는 있었습니다.
하지만 진입장벽이 낮기 때문에 접하기 쉽고 그만큼 많이 사용되는 듯합니다.

Stylus 같은 경우는 현재 이 블로그(HEROPY)를 만들면서 사용하고 있습니다.
깔끔하고 좀 더 세련됐으며 기능도 훌륭합니다.
하지만 덜 사용되며(덜 유명하며) 비교적 늦게 나왔기 때문에 성숙도는 떨어집니다.
그 때문인지 컴파일 후 사소한 버그가 몇몇 보입니다.

Sass(SCSS)는 언급한 두 가지 전처리기의 장점을 모두 가집니다.
문법은 Sass가 Stylus와 비슷하고, SCSS는 Less와 비슷하며, Sass와 SCSS는 하나의 컴파일러로 모두 컴파일 가능합니다.
또한, 2006년부터 시작하여 가장 오래된 CSS 확장 언어이며 그만큼 높은 성숙도와 많은 커뮤니티를 가지고 있고 기능도 훌륭합니다.
그래서 저는 Sass(SCSS)를 선택했습니다.



### Sass와 SCSS는 차이점은 뭔가요?

Sass에서 나온 SCSS는 CSS 구문과 완전히 호환되도록 새로운 구문을 도입해 만든 Sass의 모든 기능을 지원하는 CSS의 상위집합(Superset) 입니다.

즉, SCSS는 CSS와 거의 같은 문법으로 Sass 기능을 지원한다.

​	SCSS  > Sass > CSS



**CSS**

```
/**CSS Syntax**/

nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

**Sass**

```
/**Sass Syntax**/

nav
  ul
    margin: 0
    padding: 0
    list-style: none

  li
    display: inline-block

  a
    display: block
    padding: 6px 12px
    text-decoration: none
```



다른 예시



**- CSS**

```css
.list {  
    width: 100px;  float: left;  
} 
li {  
    color: red;  background: url("./image.jpg");  
} 
li:last-child {  
    margin-right: -10px;  
}
```



**- SCSS**

```scss
.list {  
    width: 100px;  float: left;  
    li {    color: red;    
        	background: url("./image.jpg");    
        	&:last-child {      margin-right: -10px;    
        }  
    } 
}
```



**- SASS**

: 괄호와 ;가 사라진다.

```SASS
.list  
	width:100px  
	float: left  
	li    
		color: red    
		background:url("./image.jpg")
		&:last-child      
			margin-right:-10px
```

