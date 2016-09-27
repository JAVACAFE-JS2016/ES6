# Arrow 표기법(=>)

1. function의 사용을 간소화하는 기능
2. arrow 표기법에서 사용하는 this는 렉시컬 바인딩
  1. 기존 함수에서의 this
    * 생성자인 경우는 신규 객체
    * 엄격모드에서는 함수에서 호출 시에는 undefined, 일반은 window
    * 객체 메소드에서 호출 시에는 객체
    ```javascript
    function Test() {
      console.log(this);
    }
  
    let aaa = new Test();   // this는 aaa(생성자 호출)
  
    function test() {
      console.log(this);
    }
  
    test();                  // this는 window(함수 호출)
    
    var obj = {
      fun : function() {
        console.log(this);
      }
    };
    
    obj.fun();              //this는 obj 자신(객체 메소드)
    var func2 = obj.fun();
    func2();                //this는 window(함수 호출로 인식)
    // 매우 다양한 this로 인해서 혼란 가중
    ```
  2. arrow 표현법에서의 this는 렉시컬 this
    1. 렉시컬 this : 주의 코드의 this를 그대로 사용 
3. 항상 익명으로 처리
4. 생성자로서 사용할 수 없음(new 사용 불가)
  ```javascript
  const sum1 = function(a,b) {
    return a + b;
  }
  const sum1 = (a,b) => a + b;  // 표현 식의 경우는 return을 생략해서 표현 가능
  const sum2 = a => a; // 파라미터가 1개인 경우에는 () 생략 가능
  const sum3 = (a,b) => {
    return a + b;
  }               // 표현 문을 사용할 경우는 return 이 필요.
  
  // Lexical this
  var bob = {
    _name: "Bob",
    _friends: [],
    printFriends() {
      this._friends.forEach(f =>
        console.log(this._name + " knows " + f));   //this는 obj 자신
    }
    aaa : () => console.log(this)         //this 는 window, 이해는 되는데 설명이 힘듬;
  };
  ```
5. [모질라링크](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)
6. [lexical this에 대한 설명](http://www.2ality.com/2012/04/arrow-functions.html) 

