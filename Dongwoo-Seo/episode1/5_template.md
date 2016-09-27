# Template literals

1. 자바스크립트에서 기본적으로 template 을 제공
2. 이전 외부 라이브러리보다 쓰기가 더 편한 듯
3. 행변환 등을 지원
  ```javascript
  const aaa= 100;
  const bbb= 200;
  const ccc= 300;

  console.log(`
    aaa : ${aaa},
    bbb : ${bbb},
    ccc : ${ccc}
  `);     //`` 기호를 사용해서 처리, ${변수명}으로 기존 변수를 사용할 수 있음
  ```
4. Tagged template literals
  1. 첫 번째 argument에 string literals
  2. 두 번째 argument 부터는 표현 식들을 저장
  ```javascript
  function tag(strings, ...values) {
    console.log(strings[0]); // "Hello "
    console.log(strings[1]); // " world "
    console.log(strings[2]); // ""
    console.log(values[0]);  // 15
    console.log(values[1]);  // 50

    return "Bazinga!";
  }

  tag`Hello ${ a + b } world ${ a * b }`;
  // "Bazinga!"
  
  function customtags(String, ...values) {
    return function(...datas) {
      return ``;
    }
  }
  
  function tempate(strings, ...values) {
    console.log(strings[0]);  //""
    console.log(strings[1]);  //""
    console.log(strings[2]);  //"!"
    console.log(values[0]); //3
    console.log(values[1]); //5
    console.log(values[2]); //undefined
  }

  tempate`${1+2}${2+3}!`
    
  function template(strings, ...keys) {
    return (function(...values) {
      var dict = values[values.length - 1] || {};
      var result = [strings[0]];
      keys.forEach(function(key, i) {
        var value = Number.isInteger(key) ? values[key] : dict[key];
        result.push(value, strings[i + 1]);
      });
      return result.join('');
    });
  }

  var t1Closure = template`${0}${1}${0}!`;
  t1Closure('Y', 'A');  // "YAY!" 
  var t2Closure = template`${0} ${'foo'}!`;
  t2Closure('Hello', {foo: 'World'});  // "Hello World!"
  
  `Hi\n${2+3}!`         //Hi
                        //5!
  String.raw`Hi\n${2+3}!`;  //Hi\n5!
  ```
