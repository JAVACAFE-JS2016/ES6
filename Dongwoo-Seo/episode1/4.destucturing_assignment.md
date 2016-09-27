# 비구조화 할당(destructuring assignment)

1. 배열 또는 객체에서 데이터를 별개 변수로 추출할 수 있게 하는 javascript expression

  ```javascript
  let a=10;
  let b=20;
  const d='2222';

  const c = {
      a     // a:a 와 같이 property 명과 변수 명이 같은 경우 하나로 통일 가능
      ,b    // b:b
      ,[d+'1'] : 40   //d1:40 와 같이 동적으로 식 표현이 가능
      ,[d+'2'] : 30   //d2:30
  };
  
  const k = {
      aaa() { //aaa : function() {  : function() { 생략 해서 표현 가능

      }, bbb() { //bbb : function() {

      }
  }
  
  let [a,b] = [b,a];
  //temp=a; a=b; b=temp;
  const [f,g,h,,u] = [1,2,3,4,5];
  // f=1, g=2, h=3, u=5와 같이 표현 가능 4는 assign 하는 변수명이 없기 때문에 생략
  
  const obj = {
    a:100,
    b:200,
    c:300,
    d:400,
    e:500
  }
  
  //동일한 변수 명 매핑
  var a, b, c, d, e;
  a = obj.a;
  b = obj.b;
  c = obj.c;
  d = obj.d;
  e = obj.e;
  
  let {a,b,c,d,e} = obj
  
  //동일하지 않는 변수 명 매핑
  var a1, b1, c1, d1, e1;
  a1 = obj.a;
  b1 = obj.b;
  c1 = obj.c;
  d1 = obj.d;
  e1 = obj.e;
  
  let {a:a1,b:b1,c:c1,d:d1,e:e1} = obj


  //객체의 뎁스가 여러 개인 경우
  const obj = {
    a:100,
    b:200,
    c:{f : 30},
    d:400,
    e:500
  }
  
  var a1, b1, f1, d1, e1;
  a1 = obj.a;
  b1 = obj.b;
  f1 = obj.c.f;
  d1 = obj.d;
  e1 = obj.e;
  
  let {a:a1,b:b1,c:{f:f1},d:d1,e:e1} = obj
  
  //함수 파라미터 배열 매핑
  function f([name, val]) {
    console.log(name);
    console.log(val);
  }

  function g({name :n, value: v}) {
      console.log(n);
      console.log(v);
  }
  ```
