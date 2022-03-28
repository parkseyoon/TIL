# Javascript Immutability

## Immutability란?
불변성을 의미하고, 데이터의 원본이 훼손되는 것을 막는 것.

<br>

### 데이터를 불변하게 다루면 어떤점이 좋느냐.
1. 데이터들 간의 간섭으로 인한 버그의 가능성을 획기적으로 낮출 수 있다.
2. 데이터가 변경되었는지 여부를 매우 쉽게 체크할 수 있다.
3. CRUD(Create, Read, Update, Delete) 작업 시, 불변성을 보장하는 것은 ⭐️매우 중요⭐️

<br>

## 이름에 대한 불변함
```js
var v = 1; // v는 name, 1은 value를 뜻함.
v = 2;
console.log(v); // 2

const a = 1;
a = 2; // error
```

이름을 불변하게 하는 방법은 바로 `const`를 사용하는 것이다.
const를 사용하게 되면 선언한 변수를 <b>수정</b>할 수 없게 되며, 수정을 시도하는 경우 <b>error</b>를 발생시킨다.

## 내용에 대한 불변함

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWTPfU%2FbtqCkRfyuQv%2FgqNBKrdRabkweGYPiPvt81%2Fimg.png)

```js
var p1 = 1;
var p2 = 1;
console.log(p1===p2); // true

var o1 = {name:'kim'}
var o2 = {name:'kim'}
console.log(o1===o2); // false
```
JavaScript는 값이 바뀌지 않는 원시 데이터 타입과 값이 바뀔 수 있는 객체 타입(Object)을 다르게 취급한다.


### `Data Type`
- 원시 데이터 타입 (Primitive) : Number, String, Boolean, Null, Undefined, Symbol...
- 객체 타입 (Object) : Object, Array, Function...

<br>

## 객체의 복사

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbbs9dn%2FbtqCl9thA3P%2F9aEiZZK0uofChU6UkTEWp0%2Fimg.png)

```js
var o1 = {name:'kim'}
var o2 = Object.assign({}, o1) // 첫 번째 파라미터와 두 번째 파라미터를 합쳐서 return
o2.name = 'lee';
console.log(o1, o2, o1==o2); // {name:'kim'} {name:'lee'} false
```

<br>

## 원본 객체를 수정하지 않고 복제본을 수정하는 방법

```js
var o1 = {name:'kim', score:[1,2]}
var o2 = Object.assign({}, o1);
o2.score = o2.score.concat(); // o2.score를 복제
o2.score.push(3);
console.log(o1, o2, o1 === o2, o1.score === o2.score);
// {name:'kim', score:[1,2]} {name:'kim', score:[1,2,3]} false false
```

### Nested Data의 복제 `(concat)`

Object가 Object 형태로 내부 property를 갖고 있는 경우 <b>Nested Data (중첩된 데이터)</b>라고 부른다.
아래와 같이 Array(Object)를 property로 가지고 있는 경우, 해당 값 변경 시 원본 데이터 값이 영향을 받게 된다. 따라서 Object와 내부 property 값도 복제(concat)해서 사용해야 원본 데이터를 유지할 수 있다.

Javascript는 함수의 파라미터의 인자가 원시 데이터인지 객체인지에 따라 동작 방법이 달라진다.
따라서 아래와 같이 함수를 정의할 때 원본 데이터를 유지할 것인지 아닌지에 따라 `assign`, `concat` 함수를 통해 불변성을 유지해야 한다. 

```js
// function fn(person){
//     person = Object.assign({}, person);
//     person.name = 'lee';
//     return person;
// }
// var o1 = {name:'kim'}
// var o2 = fn(o1);
// console.log(o1, o2);
 
function fn(person){
    person.name = 'lee';
}
var o1 = {name:'kim'}
var o2 = Object.assign({}, o1);
fn(o2);
console.log(o1, o2); // {name:'kim'} {name:'lee'}
var score = [1,2,3];
var a = score;
var b = score;
// 1~
// score.push(4);
var score2 = score.concat(4);
console.log(score, score2, a, b); // [1,2,3] [1,2,3,4] [1,2,3] [1,2,3]
```

<br>

## `const` vs `Object.freeze`

const : <b>name이 가르키는 값</b>을 다른 것으로 못 바꾸게 하는 것 <br>
Object.freeze : <b>값 자체</b>를 못 바꾸게 하는 것