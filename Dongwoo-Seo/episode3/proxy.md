#Proxy

## Proxy란?

Proxy Object는 자바스크립트에서 일반적으로 사용하는 기본적인 행위들(property lookup, assignmenet, enumveration, 함수 실행)을 사용자가 임의로 정의해서 만들 수 있는 객체

## 관련용어

  1. hander
  traps를 포함한 대리자 객체
  2. traps
  프로퍼티 연결을 제공하는 메소드
  3. target
  해당 기능을 저장해 놓는 ojbect

## 문법

```javascript
var  p = new Proxy(target, handler);

```

## 핸들어 종류

  1. handler.getPrototypeOf()
  A trap for Object.getPrototypeOf.
  2. handler.setPrototypeOf()
  A trap for Object.setPrototypeOf.
  3. handler.isExtensible()
  A trap for Object.isExtensible.
  4. handler.preventExtensions()
  A trap for Object.preventExtensions.
  5. handler.getOwnPropertyDescriptor()
  A trap for Object.getOwnPropertyDescriptor.
  6. handler.defineProperty()
  A trap for Object.defineProperty.
  7. handler.has()
  A trap for the in operator.
  8. handler.get()
  A trap for getting property values.
  9. handler.set()
  A trap for setting property values.
  10. handler.deleteProperty()
  A trap for the delete operator.
  11. handler.ownKeys()
  A trap for Object.getOwnPropertyNames.
  12. handler.apply()
  A trap for a function call.
  13. handler.construct()
  A trap for the new operator.
  
자세한 건 아래 링크들 참고

* https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy  
* http://hacks.mozilla.or.kr/2016/03/es6-in-depth-proxies-and-reflect/


## 예

```javascript
var handler = {
    get: function(target, name){
        return name in target?
            target[name] :
            37;
    }
};

var p = new Proxy({}, handler);
p.a = 1;
p.b = undefined;

console.log(p.a, p.b); // 1, undefined
console.log('c' in p, p.c); // false, 37

//숫자만 등록 가능하게 구성
let numberHandler = {
  set: function(target, property, value, receiver) {
    if (!Number.isInteger(value)) {
        throw new TypeError('숫자가 아니에요.');
    }
  }
};

let p = new Proxy({}, numberHandler);

p.a = 100;
p.b = 'aaa';

/*
  var docCookies = ... get the "docCookies" object here:  
  https://developer.mozilla.org/en-US/docs/DOM/document.cookie#A_little_framework.3A_a_complete_cookies_reader.2Fwriter_with_full_unicode_support
*/

var docCookies = new Proxy(docCookies, {
  get: function (oTarget, sKey) {
    return oTarget[sKey] || oTarget.getItem(sKey) || undefined;
  },
  set: function (oTarget, sKey, vValue) {
    if (sKey in oTarget) { return false; }
    return oTarget.setItem(sKey, vValue);
  },
  deleteProperty: function (oTarget, sKey) {
    if (sKey in oTarget) { return false; }
    return oTarget.removeItem(sKey);
  },
  enumerate: function (oTarget, sKey) {
    return oTarget.keys();
  },
  ownKeys: function (oTarget, sKey) {
    return oTarget.keys();
  },
  has: function (oTarget, sKey) {
    return sKey in oTarget || oTarget.hasItem(sKey);
  },
  defineProperty: function (oTarget, sKey, oDesc) {
    if (oDesc && "value" in oDesc) { oTarget.setItem(sKey, oDesc.value); }
    return oTarget;
  },
  getOwnPropertyDescriptor: function (oTarget, sKey) {
    var vValue = oTarget.getItem(sKey);
    return vValue ? {
      value: vValue,
      writable: true,
      enumerable: true,
      configurable: false
    } : undefined;
  },
});

/* Cookies test */

console.log(docCookies.my_cookie1 = "First value");
console.log(docCookies.getItem("my_cookie1"));

docCookies.setItem("my_cookie1", "Changed value");
console.log(docCookies.my_cookie1);

```
