# Parameter

1. 전개 연산자(spread operator)
  1. 식이 여러 인수나 여러 요소 또는 여러 변수가 예상되는 곳에 확장될 수 있도록 함
    ```javascript
    const test = (a,b,...c) => (a + b) * c.length;
    console.log(test(1,2,3,4,5,'dwdwwdwdw');  // (1 + 2) * 4 = 12
                                                // 1은 a 값, 2는 b 값 4는 c([3,4,5,'...'] 배열)의 length
    const param = [1,2,3];
    const param2 = [4,5,...param]; // [4,5,1,2,3]
    //param.concat(param2);         //같은 결과

    const param3 = [2,3,4,...param,5,6,7];  //[2,3,4,1,2,3,5,6,7];
    //const param4 = [2,3,4,5,6,7];
    //param4.splice(3,0, param);    //같은 결과
    ```
  2. arguments 등 직관적으로 알기 힘든 객체를 데체해서 사용 가능
    ```javascript
    function oldTest() {
      const a = arguments[0];
      const b = arguments[1];
      const c = arguments[2];

      return a + b + c;
    }

    function test(...args) {
      const a = args[0];
      const b = args[1];
      const c = args[2];

      return a + b + c;
    }
    ```
  3. 동적으로 parameter 를 사용할 때도 좋다.
  
    ```javascript
    function myFunction(x,y,z) {}
    var args = [0,1,2];
    myFunction.apply(null, args);   //예전방식
    myFunction(...args);            //이렇게도 쓸 수 있다.
    ```
    
2. default value 사용이 가능
  ```javascript
  function oldSum(a,b,c) {

      if (a === null) { a=10; }
      if (b === null) { b=20; }
      if (c === null) { c=30; }

      return a+b+c;
  }

  const sum = (a=10, b=20, c=30) => a+b+c;

  console.log(sum());     // 10 + 20 + 30
  console.log(sum(100));  // 100 + 20 + 30
  console.log(sum(100, 200)); //100 + 200 + 30
  console.log(sum(100, 200, 300));  //100 + 200 + 300
  ```
