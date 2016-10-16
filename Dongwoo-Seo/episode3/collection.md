# collection

## collection을 왜 만들었을까요?

1. 일반 자바스트립트에서는 hash table과 비슷한 것이 존재한다.(object)
2. object 만으로 무언가 부족한 것들이 있다.

  - 키 값을 문자열과 심볼만 가능하다.
  - 이미 존재하는 객체 속성을 검색할 수 이는 방법이 없다.
  - 가장 중요한 부분 객체는 이터러블하지 않다!

3. 위 object의 문제점을 해결하기 위해 map, set과 같은 collection이 나왔다!

## collection 들의 공통적인 특징

1. 자신의 맴버 데이터에 접근하기 위해 속성 값을 직접 호출하는 방식이 아닌 get 매소드를 이용한다.
2. 프로퍼티 체인을 통해 상속되지 않는다.

## Set

1. value 들로 이루어진 컬렉션
2. set은 수정 가능
3. 동일한 value가 들어갈 수 없다.
4. 어떤 데이터가 자신의 맴버인지를 빠르게 검색할 때 사용

```javascript
const numbers = new Set();

numbers.add(10);
numbers.add(20);
numbers.add(30);
numbers.add(40);
//[10,20,30,40]

numbers.add(10);
//[10,20,30,40]
numbers.delete(10);
//[20,30,40]

numbers.has(10)
//false

number.size() //3
number.clear() // []


const strings = new Set('aabbbcccc');
// Set['a', 'b', 'c']
```

## Map

1. key-value 페어로 이루어진 컬렉션 ```javascript const map = new Map();

map.set('aaa', 100); map.set('bbb', 200); map.has('aaa'); map.size(); map.delete('aaa'); map.clear(); ```

## Weak?

1. 이건 Map, Set의 경우는 강한 참조이기 때문에 아래와 같은 경우에도 GC에서 제거되지 않는다.

  1. DOM의 객체를 Map이나 Set에 등록
  2. DOM 객체를 삭제
  3. Map, Set에서 해당 DOM 객체를 찾아서 같이 삭제해주지 않는 경우 해당 DOM은 Map이나 Set에서 사용 중이기 때문에 GC에서 수거 대상에서 제외

2. 해당 문제를 해결하기 위해서 WeakSet, WeakMap이 나왔으며 이들은 객체만 등록이 가능
3. 기능은 거의 Map이나 Set과 비슷하지만 열거형이 아니라는 점이 차이
4. 그럼 언제 weak 를 사용하나? 아래 간단한 예제가 있다.

```javascript
const privates = new WeakMap();

function Public() {
  const me = {
    // Private data goes here
  };
  privates.set(this, me);
}

Public.prototype.method = function () {
  const me = privates.get(this);
  // Do stuff with private data in `me`...
};

module.exports = Public;
```
