# 코딩 컨벤션

모든 코드는 ES6를 기준으로 작성한다.

## 들여쓰기

space와 tab을 섞어서 사용하지 않는다. 공백 문자는 2개로 통일한다.

## 문장의 종료

한 줄에 하나의 문장만 허용하며, 문장 종료 시에는 반드시 세미콜론(;)을 사용한다.

## 명명 규칙

변수, 함수에는 카멜 케이스(Camel case)을 사용한다.

```js
// 숫자, 문자, 불린
let dog;
let variableName;

// 배열 - 배열은 복수형 이름을 사용
const dogs = [];

// 정규표현식 - 정규표현식은 'r'로 시작
const rDesc = /.*/;

// 함수
function getPropertyName() {
  ...
}

// 이벤트 핸들러 - 이벤트 핸들러는 'on'으로 시작
const onClick = () => {};
const onKeyDown = () => {};

// 불린 반환 함수 - 반환 값이 불린인 함수는 'is'로 시작
let isAvailable = false;
```

생성자는 대문자 카멜 케이스를 사용한다.

```js
class ConstructorName {
  ...
};
```

상수는 영문자 대문자 스네이크 표기법을(Snake case)를 사용한다.

```js
SYMBOLIC_CONSTANTS;
```

예약어를 사용하지 않는다.

## 전역 변수

전역 변수를 사용하지 않는다.

## 선언과 할당

### 변수

값이 변하지 않는 변수는 const를, 값이 변하는 변수는 let을 사용하여 선언한다. var는 절대로 사용하지 않도록 한다.

const를 let 보다 위에 선언한다.

const와 let은 사용 시점에 선언 및 할당을 한다.

const와 let으로 선언한 변수는 블록 스코프이므로 호이스팅(hoisting) 되지 않는다.

```js
function foo() {
  // 사용 시점에 선언 및 할당
  const len = this._array.length;
  for (let i = 0; i < len; i += 1) {
      ...
  }

  // 사용 시점에 선언 및 할당
  const len2 = this._array2.length;
  for (let j = 0; j < len2; j += 1) {
      const item = this._array2[j];
      ...
  }
}
```

외부 모듈과 내부 모듈을 구분하여 사용한다.

```js
const lodash = require('lodash');
const $ = require(jquery);
const handlebars = require('handlebars');
const d3 = require('d3');

const pluginFactory from '../../factories/pluginFactory';
const predicate from '../../helpers/predicate';
const raphaelRenderUtil from '../../plugins/raphaelRenderUtil';
```

## 배열과 객체

배열과 객체는 반드시 리터럴로 선언한다.

```js
// Bad
const emptyArr = new Array();
const arr = new Array(1, 2, 3, 4, 5);

// Bad - 객체 생성자 사용
const emptyObj = new Object();
const obj = new Object();

// Good
const emptyArr = [];
const arr = [1, 2, 3, 4, 5];

// Good
const emptyObj = {};
const obj = {
  pro1: "val1",
  pro2: "val2",
};
```

배열 복사 시 순환문을 사용하지 않는다.

복잡한 객체를 복사할 떄 전개 연산자를 사용하면 좀 더 명확하게 정의할 수 있고 가독성이 좋아진다.

```js
const len = items.length;
let i;

// Bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// Good
const itemsCopy = [...items];
```

배열의 시작 괄호 안에 요소가 줄 바꿈으로 시작되었다면 끝 괄호 이전에도 일관된 줄 바꿈 해야한다.

```js
// Bad
var a = [1];

// Good
var c = [1];
var d = [1];
```

배열의 요소 중 하나라도 줄 바꿈이 있다면 배열 안의 요소는 일관되게 모두 줄 바꿈을 해주어야 한다.

```js
const a = [1, 2, 3];
const b = [1, 2, 3];
```

객체의 프로퍼티가 1개인 경우에만 한 줄 정의를 허용하며, 2개 이상일 경우에는 개행을 강제한다.

```js
// Bad - 개행
const obj = { foo: "a", bar: "b" };

// Good
const obj = { foo: "a" };

// Good
const obj = {
  foo: "a",
};
```

객체의 메서드 표현 시 축약 메소드 표기를 사용한다.

```js
// Bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

// Good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

메서드 문법 사용 시 메서드 사이에 개행을 추가한다.

```js
// Bad
class MyClass {
  foo() {
    //...
  }
  bar() {
    //...
  }
}

// Good
class MyClass {
  foo() {
    //...
  }

  bar() {
    //...
  }
}
```

## 함수

함수 생성자를 사용하여 선언하지 않는다.

```js
// Bad - 함수 생성자 사용
const doSomething = new Function("param1", "param2", "return param1 + param2;");

// Good - 함수 선언식 사용
function doSomething(param1, param2) {
  return param1 + param2;
}

// Good - 함수 표현식 사용
const doSomething = function (param1, param2) {
  return param1 + param2;
};
```

함수는 사용 전에 선언해야 하며, 함수 선언문은 변수 선언문 다음에 오도록 한다.

함수 표현식으로 생성된 함수는 호이스팅 시 값이 할당되지 않으므로 선언 이전에 사용하면 오류가 발생한다.

```js
// Bad - 선언 이전에 사용
const sumedValue = sum(1, 2);
const sum = function (param1, param2) {
  return param1 + param2;
};

// Bad - 선언 이전에 사용
const sumedValue = sum(1, 2);
function sum(param1, param2) {
  return param1 + param2;
}

// Good
const sum = function (param1, param2) {
  return param1 + param2;
};
const sumedValue = sum(1, 2);
```

### 화살표 함수

함수 표현식 대신 화살표 함수를 사용한다.

```js
// Bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// Good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```

화살표 함수의 파라미터가 하나이면 괄호를 생략한다.

```js
// Bad
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// Good
[1, 2, 3].map((x) => x * x);

// Good
[1, 2, 3].reduce((y, x) => x + y);
```

암시적 반환은 최대한 활용한다.

함수의 본체가 하나의 표현식이면 중괄호를 생략하고 암시적 반환을 사용할 수 있다. 그 외에는 return문을 명시해야 한다.

```js
// Bad
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  `A string containing the ${nextNumber}.`;
});

// Good - 암시적 return을 사용
[1, 2, 3].map((number) => `A string containing the ${number + 1}.`);
```

암시적 반환을 사용할 경우 함수 본문 전에 개행을 하지 않는다.

```js
// Bad
(foo) => bar;

(foo) => bar;

(foo) => (bar) => baz;

// Good
(foo) => bar;

(foo) => bar;

(foo) => (bar) => baz;

(foo) => bar();
```

### Destructuring

오브젝트의 프로퍼티에 접근할 때는 Destructuring을 이용한다.

```js
// Bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// Bad
const first = arr[0];
const second = arr[1];

// Good
function getFullName(obj) {
  const { firstName, lastName } = obj;

  return `${firstName} ${lastName}`;
}

// Good
const [first, second] = arr;

// Good
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

### 템플릿 문자열

변수 등을 조합해서 문자열을 생성하는 경우 템플릿 문자열을 이용한다.

```js
// Bad
function sayHi(name) {
  return "How are you, " + name + "?";
}

// Bad
function sayHi(name) {
  return ["How are you, ", name, "?"].join();
}

// Bad - 일반적인 경우, 홑따옴표를 사용
function sayHi(name) {
  return `How are you name?`;
}

// Good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

## 클래스와 생성자

class와 extends를 이용해서 객체 생성 및 상속을 구현한다.

## 모듈

항상 import와 export를 이용한다.

wilecard import는 사용하지 않는다.

```js
// Bad
import * from './AirbnbStyleGuide';

// Good
import * as AirbnbStyleGuide from './AirbnbStyleGuide';
```

## 블록 구문

한 줄짜리 블록일 경우라도 {}를 생략하지 않으며 명확히 줄 바꿈 하여 사용한다.

```js
// Bad
if(condition) doSomething();

// Bad
if (condition) doSomething();
else doAnything();

// Bad
for(let prop in object) someIterativeFn();

// Bad
while(condition) iterating += 1;

// Good
if (condition) {
  ...
}

// Good
if (condition) {
  ...
} else {
  ...
}
```

키워드와 조건문 사이에 빈칸을 사용한다.

```js
// Bad
var i = 0;
for (; i < 100; i += 1) {
  someIterativeFn();
}

// Good
var i = 0;
for (; i < 100; i += 1) {
  someIterativeFn();
}
```

## 조건 확인하기

삼중 등호 연산자인 ===, !==만 사용한다.

## 주석

주석은 설명하려는 구문에 맞춰 들여쓰기 한다.

```js
// Bad
function someFunction() {
  ...

// statement에 관한 주석
  statements
}

// Good
function someFunction() {
  ...

  // statement에 관한 주석
  statements
}
```

문장 끝에 주석을 작성할 경우, 한 줄 주석을 사용하며 공백을 추가한다.

```js
// Bad
var someValue = data1; //주석 표시 전후 공백

// Bad
var someValue = data1; /* 여러 줄 주석 */

// Good
var someValue = data1; // 주석 표시 전후 공백
```

여러 줄 주석을 작성할 때는 \*의 들여쓰기를 맞춘다. 주석의 첫 줄과 마지막 줄은 비워둔다.

```js
// Bad - '*' 표시의 정렬
/*
* 주석내용
*/

// Bad - 주석의 첫 줄에는 기술하지 않는다
...
/* var foo = '';
 * var bar = '';
 * var quux;
 */

// Good - '*' 표시의 정렬을 맞춘다
/*
 * 주석내용
 */
```

코드 블럭 주석 처리를 위해서는 한 줄 주석을 사용한다.

```js
// Bad - 여러 줄 주석을 사용
...
/*
 * var foo = '';
 * var bar = '';
 * var quux;
 */

// Good - 한 줄 주석 사용
...
// var foo = '';
// var bar = '';
// var quux;
```

# 참조

[TOAST UI FE개발랩](https://ui.toast.com/fe-guide/ko_CODING-CONVENTION)
