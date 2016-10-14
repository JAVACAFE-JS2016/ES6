# Symbol

## 7번째 타입

기존 자바스크립트는 총 6개의 타입으로 구성

1. undefined
2. null
3. boolean
4. number
5. string
6. obejct

Symbol은 위 6개의 타입과는 다른 새로운 타입
``` javascript
const aaaa = Symbol('test');

typeof aaaa;

```

## 그래서 심볼은 머야?

1. 이름 충의 위험 없이 속성(property)의 키(key)로 쓰기 위해 생성하고 사용할 수 있는 값
2. 사용 방법
  ```javascript
  const mySymbol = Symbol('tester!!!');    //여기서 tester는 주석의 역할
  
  const obj = {};
  obj[mySymbol] = 'true';
  console.log(obj[mySymbol]);
  obj.mySymbol //에러 이렇게는 사용 못함

  const symbol = Symbol('aaaa');
  const symbol2 = Symbol.for('aaaa');  //심볼 레지스트리에 등록
  const symbol3 = Symbol.for('aaaa');  //이미 등록되어 있는 경우에는 그것을 받아와서 사용
  
  Symbol.keyFor(symbol3);	//aaaa 심볼의 키를 반환

  symbol !== symbol2
  symbol3 !== symbol2

  Symbol.iterator //표준에 의해 정의된 심볼

  ```
3. 생성된 심볼은 어떤 다른 값과도 다르다.(주석에 같은 값을 해도 다른 심볼)
  ```javascript
  const mySymbol = Symbol('test');
  const mySymbol2 = Symbol('test');
	

  mySymbol !== mySymbol2

  ```
4. 실행 스코프 안에 있을 때만 사용 가능
5. for-in 등과 같은 일반적인 객체 조사에서는 전부 무시, 심볼 조사를 위해서는 아래와 같은 API를 사용
```javascript
  const obj = {};
  obj[mySymbol] = 'true';

  for(let pro in obj) {
    //심볼을 못찾음
  }

  Object.getOwnPropertySymbols(obj);//심볼 리스트를 받을 수 있음
   
```
6. 한번 생성되면 변경이 되지 않는다.
7. 심볼에서는 속성을 부여할 수 없다.
8. Symbol value
  primitive value that represents a unique, non-String Object property key
9. Symbol type
  set of all possible Symbol values
10. Symbol object
  member of the Object type that is an instance of the standard built-in Symbol constructor
11. new 키워드를 이용한 생성을 막고 있다. 기본형 변수에 대해 명시적 레퍼 객체를 만드는 것은 ES2016에서 지원하지 않음. 예외로 이전부터 사용하던 것들은 하위 호환성을 위해서 유지
```javascript
const aaa = new Symbol('aaaa'); //type error
```
12. 잘 알려진 심볼들
  * Symbol.iterator
  * Symbol.match
  * Symbol.replace
  * Symbol.search
  * Symbol.split
  * Symbol.hasInstance
  * Symbol.isConcatSpreadable
  * Symbol.unscopables
  * Symbol.species
  * Symbol.toPrimitive
  * Symbol.toStringTag
  아직 거의 구현되어 있지는 않음.
  
## 그럼 왜?

1. 시로운 기능과 예전 코드의 충돌을 제거



