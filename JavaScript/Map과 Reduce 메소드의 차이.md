## Map과 Reduce 메소드의 차이

> 두 함수는 자바스크립트에서 자주 사용되는 배열 메소드이며, 평소 Map 함수를 즐겨 사용하고 있다. Map 함수와 Reduce 함수의 차이에 대해 간단히 알아본다.

### Map

> map() 메소드는 배열의 모든 요소들을 순회하며 주어진 콜백 함수를 실행시킨다. 콜백함수에서 반환된 값들은 배열 형태로 정리되어 최종 반환된다.

```js
let arr = [1, 2, 3, 4, 5];

// 화살표 함수를 지원하며, 아래 두 경우 반환 값은 동일하다.
// 콜백함수 내의 el 변수에는 배열 각 요소들이 차례대로 담기게 된다.
let double1 = arr.map(function(el){
    return el*2
})

let double2 = arr.map(el => el * 2)

console.log(double1,double2)
//[2, 4, 6, 8, 10], [2, 4, 6, 8, 10] 
```

- 특이점은 따로 빈 배열을 선언하지 않고, `push()`하지 않아도 배열형태로 반환이 된다는 것, 그리고 배열의 길이도 달라지지 않는다는 것이다.
- 배열의 길이를 바꾸지 않고, 배열 내의 요소들에만 변화를 주고 싶을 때 활용할 수 있다.

### Reduce

> reduce()메소드는 배열의 모든 요소들을 순회하면서 주어진 리듀서 함수(콜백 함수)를 실행시킨다. 리듀서 함수의 필수 파라미터로 accumulator, currentValue과 있는데, 리듀서 함수에서 반환된 값은 accumulator에 할당된다. accumulator는 배열 순회 중 유지되며, 모든 배열의 요소의 순회가 끝났을 때 최종적으로 반환된다.

```js
let arr = [1, 2, 3, 4, 5];

// 마찬가지로 화살표 함수 지원
let sum1 = arr.reduce((acc,cur)=>acc+cur)
let sum2 = arr.reduce((acc,cur)=>acc+cur,10)

console.log(sum1, sum2)
// 15, 25
```

- `reduce()` 메소드의 파라미터로는 첫 번째(필수)로 reducer함수(콜백)를, 두 번째(선택)로 initialValue를 받는다.
- 만약 initialValue가 별도로 할당이 되어있다면, reducer 함수의 accumulator initialValue, currentValue는 배열의 첫 번째요소부터 시작한다.
- initialValue가 별도로 할당되어 있지 않다면 accumulator는 배열의 첫 번째 요소, currentValue는 배열의 두 번째 요소부터 시작한다.
- 특이점은 최종 반환되는 값이 accumulator이기 때문에 `map()`메소드 처럼 배열의 형태가 아닐 수 있다는 것이다. initialValue로 어떤 값을 주느냐에 따라 배열이나 객체 형태로 반환이 될 수도 있고, 예시에서처럼 숫자로 반환시킬 수도 있다.
- 배열의 형태에서 원하는 형태(객체, 배열, 숫자, 문자 등)로 값을 변환시키고 싶을 때 활용할 수 있다.