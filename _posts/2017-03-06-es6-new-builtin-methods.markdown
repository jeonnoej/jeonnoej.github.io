---
layout: post
title:  "[ES6] New Built-in Methods"
date:   2017-03-06 13:47:00 +0900
---

# New Built-in Methods
## Object
 * Object Property Assignment
    * 프로퍼티를 복사한다.
    * 열거할 수 있는 소스 오브젝트의 프로퍼티만을 복사한다. enum type.
    * 내부적으로 source Object의 get, target Object의 set을 호출하여 실행한다.
    * null, undefined를 반환하지 않는다.
    * 오브젝트의 참조를 복사하므로 깊은 복사에 적합하지 않다.
    * 원시 타입은 객체로 변환된다.

```javascript
    //var target = jQuery.extend(true, {}, sourceObejcts)
    Object.assign(target, ...sourceObejcts);

    var v1 = 'abcefg';
    var v2 = true;
    var v3 = 10;
    var v4 = Symbol('foo');
    
    var obj = Object.assign({}, v1, null, v2, undefined, v3, v4);
    console.log(obj); //Object {0: "a", 1: "b", 2: "c", 3: "e", 4: "f", 5: "g"}
    //String wrapper만 enumberable property를 가진다.
```

## Array
 * Array Element Finding
    * 배열에서 특정 엘리먼트를 찾는다.
    * Callback에 조건식이 리턴되는 경우 조건에 만족하는 첫번째 엘리먼트가 반환된다.
    * 조건에 만족하는 엘리먼트가 없는 경우 undefined가 반환된다.
    * 조건식이 없을 경우 탐색한다.
    * see also
      - findIndex : 조건에 만족하는 엘리먼트의 인덱스가 반환된다.
      - every : 모든 요소가 조건을 만족하는지 검사한다.
      
```javascript
  [].find(function(element, index, array) {
      console.log(element);
      console.log(index);
      console.log(array);
  });

//ES5
  [ 1, 3, 4, 2 ].filter(function (x) {
      return x > 3;
  })[0];
  
//ES6
  [ 1, 3, 4, 2 ].find(x => x > 3)
```

## String
 * String Repeating
    * 문자열을 반복한다.
```javascript
//ES5
  Array((4 * depth) + 1).join(" ");
  Array(3 + 1).join("foo");
  
//ES6
  " ".repeat(4 * depth)
  "foo".repeat(3)
```
 * String Searching
    * String.startsWith('검색할 문자열', 찾기 시작할 위치 [default 0])
    * String.endsWith('검색할 문자열', 찾고자 하는 문자열의 길이 [default 문자열 전체 길이])
    * String.includes('검색할 문자열', 찾기 시작할 위치 [default 0])
    * 전부 대소문자 구분
```javascript
//ES6
  "hello".startsWith("ello", 1) // true
  "hello".endsWith("hell", 4)   // true
  "hello".includes("ell")       // true
  "hello".includes("ell", 1)    // true
  "hello".includes("ell", 2)    // false
```

## Number
 1. Number Type Checking
    * isNaN() : 숫자인지 아닌지 판별
    * isFinite() : 유한한 값인지 판별
```javascript
//ES5
  var isNaN = function (n) {
      return n !== n;
  };
  var isFinite = function (v) {
      return (typeof v === "number" && !isNaN(v) && v !== Infinity && v !== -Infinity);
  };
  
//ES6
  Number.isNaN(NaN) === true
  Number.isFinite(Infinity) === false
```
 2. Number Safety Checking
    * 유효한 정수 값인지 판별
```javascript
//ES5
  function isSafeInteger (n) {
      return (
             typeof n === 'number'
          && Math.round(n) === n
          && -(Math.pow(2, 53) - 1) <= n
          && n <= (Math.pow(2, 53) - 1)
      );
  }

//ES6
  Number.isSafeInteger(42) === true
  Number.isSafeInteger(9007199254740992) === false
```
 3. Number Comparison
    * Number.EPSILON 부동소수점을 비교
    * 표시할 수 있는 가장 작은 수
 4. Number Truncation
    * 양수, 음수에 상관없이 소수점 아랫 자리를 버린다.
```javascript
//ES5
  function mathTrunc (x) {
      return (x < 0 ? Math.ceil(x) : Math.floor(x));
  }

//ES6
  console.log(Math.trunc(42.7)) // 42
  console.log(Math.trunc( 0.1)) // 0
  console.log(Math.trunc(-0.1)) // -0
```
 5. Number Sign Determination
    * Math.sign : -0 / 0 / -1 / 1 / NaN
```javascript
//ES5
  function mathSign (x) {
      return ((x === 0 || isNaN(x)) ? x : (x > 0 ? 1 : -1));
  }
  
//ES6
  console.log(Math.sign(7))   // 1
  console.log(Math.sign(0))   // 0
  console.log(Math.sign(-0))  // -0
  console.log(Math.sign(-7))  // -1
  console.log(Math.sign(NaN)) // NaN
```