---
layout: post
title: "제이쿼리 물결 연산자 ( tilde 연산자 )"
description: "물결(~) 과 물결물결(~~) 연산자 사용법"
categories: js
author: Ari Kim
date: 2017-04-14 16:52:00
tags: [js, indexof, floor]
comments: true
---
## 1. tilde( ~ ) 연산자
-(n+1) 의 결과를 출력합니다.

```javascript
var val1 = 1234;
var val2 = -25;

console.log(~val1);
console.log(~val2);

> -1235
> 24
```

indexOf 로 응용할 수도 있습니다.

- 1 line : `하` 라는 글자가 str1 에 어느위치에 있는지 알려줍니다.
- 4 line : `오` 라는 글자는 str1 에 없기 때문에 0 을 출력합니다.
- 2, 5 line : ! 가 있기때문에 반대로 알려줍니다.

```javascript
var str1 = '안녕하세요.';
var str2 = '하';
var str3 = '오';

console.log(~str1.indexOf(str2));
console.log(!~str1.indexOf(str2));
console.log('---');
console.log(~str1.indexOf(str3));
console.log(!~str1.indexOf(str3));

> -3
> false
> ---
> 0
> true
```

## 2. double tilde( ~~ ) 연산자
`Math.floor()` 과 비슷한 기능입니다.

양수에서는 결과가 같으나 음수에서 차이가 보입니다.

```javascript
var num1 = 1234.5678;
var num2 = -5.9;

console.log(Math.floor(num1));
console.log(~~num1);
console.log('---');
console.log(Math.floor(num2));
console.log(~~num2);

> 1234
> 1234
> ---
> -6
> -5
```

참고 블로그
---
- [Web Club :: 틸트(~) 연산자와 물결물결(~~) 연산자](http://webclub.tistory.com/21)
- [Stack Overflow :: what-is-the-double-tilde-operator-in-javascript](http://stackoverflow.com/questions/5971645/what-is-the-double-tilde-operator-in-javascript/5971689)
