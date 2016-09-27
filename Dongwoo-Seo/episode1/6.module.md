# module

1. 자바스크립트에서 모듈화를 지원해 줌
2. 하지만 아직까지는 지원하는 브라우져가 없기 때문에 사용할 수 있는 곳이 없음
  ```javascript
  // file1.js
  export const foo = Math.sqrt(2);  // 변수 export 가능
  export function test1() {         // 함수 export 가능
    return 11111;
  }
  export default (a) => console.log('test');    //default export
  
  // file2.js
  import {foo} from './file1.js';  //변수나 함수 export시 object 매칭으로 가능
  import a from './file1.js';     // default export의 경우는 그냥 받아옴
  import {test1} from './file1.js';   
  import * as test from './file1.js';   // default를 제외한 변수 함수를 전부 export 해옴
  import a, * as test from './file1.js';  // default + 변수 함수 export 해오는 함수
  
  foo;  //4
  a();  //test
  console.log(test1()); //11111
  test.foo; //4
  test.test1() // 11111
   
  ```
