# const와 let vs var

1. var의 문제
  1. hoisting
  ```javascript
    console.log(a);    // 에러가 아닌 undefined
    var a= 10;
  ```
  2. function scope
  3. 엄격(strict mode)모드가 아닌 경우에 재 선언 가능
  ```javascript
  var a=10;
  
  if (true) {
    var a=20;       //재선언이 가능(strict mode에서는 에러)
    console.log(a); //20
  }
  
  console.log(a);   //20
  ```
2. let
  1. block({}) scope
  2. hoisting이 발생하지 않는다.
  3. 재선언 시에 에러가 발생
  4. 초기화 필수
  5. https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/let
  ```javascript
  let a=10;
  
  if (true) {
    let a=20;  
    console.log(a); //20
  }
  
  console.log(a);   //10
  let a=20;   //에러 발생
  
  console.log(c);   //hoisting 이 발생하지 않기 때문에 에러 발생
  let c=100;
  ```
3. const
  1. let과 기능의 거의 비슷
  2. reassign 이 되지 않는 점만 다름
  3. https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/const
  ```javascript
  const a= 1000;
  a=200;    //에러, reassign이 되지 않는다.
  const arr = [];
  arr.push('1111');   //에러가 발생하지 않는다. reassign 만 불가능한 것이지 변하지 않는 다는 것을 의미하지 않는다.
  const obj = {};
  obj.test = 100;     //에러가 발생하지 않는다. reassign 만 불가능한 것이지 변하지 않는 다는 것을 의미하지 않는다.
  
  const obj2;   //에러, 초기화를 하지 않았기 때문에
  ```
4. var에는 위와 같은 문제가 발생할 수 있기 때문에, ecmascript 6부터는 const나 let을 사용하기 권장
5. const와 let은 언제 사용할 것인가??
  1. const의 경우는 사용하는 변수가 reassign 을 하지 않을 때 사용
    1. ajax에서 데이터를 가져와 사용할 경우
    2. 반복문을 제외하면 왼만해서는 const로 처리가 가능할 듯
  2. let는 reassign이 필요할 경우에 사용
    1. 반복문
    
