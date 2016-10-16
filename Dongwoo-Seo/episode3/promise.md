# Promise

비동기 계산을 위해서 사용

```javascript
new Promise(function(resolve, reject) {
    //비동기 실행 함수
});
```

## 언제 사용할까요?

기존에 비동기 연산을 수행할 때 비동기 연산이 끝나고 그 결과로 다시 연산을 수행하는 경우가 있다고 생각해보자. 이럴 경우 아래와 같이 함수가 계속 중복해서 나오기 때문에 한 두개의 경우에는 크 문제가 없지만 3개 이상의 경우에는 가독성이 많이 떨어지는 것을 볼 수 있다. 이런 부분의 문제를 해결하기 위해서 Promise 를 사용한다.

```javascript
const getData = (data, callback) => setTimeout(callback, 1000);

getData(100, () => {
    console.log(100);
    getData(() => {
        console.log(100 + 200);
        getData(() => {
            console.log(100 + 200 + 300);
        }); //도대체 어디 중 괄호일 것인가..
    }); //도대체 어디 중 괄호일 것인가..
}); //도대체 어디 중 괄호일 것인가..

const promise = function(data) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log(data);
            resolve(data);
        }, 1000);
    });
};

promise(100)
.then(result => promise(result + 200))
.then(result => promise(result + 300));
```

## 단어정리

1. 상태

  - 대기중(pending) : 초기 상태, 실행되거나 거부되지 않은 상태
  - 이행됨(fullfilled, resole) : 연산이 성공적으로 완료되었음을 뜻함
  - 거부됨(reject) : 연산이 실패했음을 뜻함
  - 결론이난 상태(settled) : 약속이 되었든 안되었든 일단 결론이 난 상태

## 실행 설명

![실행 설명이미지](https://mdn.mozillademos.org/files/8633/promises.png) 비동기 함수 호출 후 결과값 또는 실패 이유를 처리하기 위한 처리기를 연결할 수 있도록 구성. ![실행 설명이미지2](http://cfile23.uf.tistory.com/image/257CF64C5444D93006ED4D)

```javascript
  asyncThing1()
    .then(function() { return asyncThing2();})
    .then(function() { return asyncThing3();})
    .catch(function(err) { return asyncRecovery1();})

    .then(function() { return asyncThing4();}, function(err) { return asyncRecovery2(); })
    .catch(function(err) { console.log("Don't worry about it");})

    .then(function() { console.log("All done!");});
```

## 사용을 한번 해봅시다.

```javascript
'use strict';

// A-> $http 함수는 표준 Adapter 패턴을 따르기 위해 구현됩니다
function $http(url){

  // 간단한 사례 객체
  var core = {

    // ajax 요청을 수행하는 메서드
    ajax: function (method, url, args) {

      // 프로미스 생성
      var promise = new Promise( function (resolve, reject) {

        // XMLHttpRequest 인스턴스화
        var client = new XMLHttpRequest();
        var uri = url;

        if (args && (method === 'POST' || method === 'PUT')) {
          uri += '?';
          var argcount = 0;
          for (var key in args) {
            if (args.hasOwnProperty(key)) {
              if (argcount++) {
                uri += '&';
              }
              uri += encodeURIComponent(key) + '=' + encodeURIComponent(args[key]);
            }
          }
        }

        client.open(method, uri);
        client.send();

        client.onload = function () {
          if (this.status >= 200 && this.status < 300) {
            // this.status가 2xx와 같은 경우 함수 "resolve" 수행
            resolve(this.response);
          } else {
            // this.status가 2xx와 다른 경우 함수 "reject" 수행
            reject(this.statusText);
          }
        };
        client.onerror = function () {
          reject(this.statusText);
        };
      });

      // 프로미스 반환
      return promise;
    }
  };

  // Adapter 패턴
  return {
    'get': function(args) {
      return core.ajax('GET', url, args);
    },
    'post': function(args) {
      return core.ajax('POST', url, args);
    },
    'put': function(args) {
      return core.ajax('PUT', url, args);
    },
    'delete': function(args) {
      return core.ajax('DELETE', url, args);
    }
  };
};
// A의 끝

// B-> 여기서 그 함수 및 payload를 정의합니다
var mdnAPI = 'https://developer.mozilla.org/en-US/search.json';
var payload = {
  'topic' : 'js',
  'q'     : 'Promise'
};

var callback = {
  success: function(data) {
    console.log(1, 'success', JSON.parse(data));
  },
  error: function(data) {
    console.log(2, 'error', JSON.parse(data));
  }
};
// B의 끝

// 메서드 호출 실행
$http(mdnAPI)
  .get(payload)
  .then(callback.success)
  .catch(callback.error);

// 메서드 호출을 실행하지만 프로미스 거부 경우를 다루는 다른 방법 (1)
$http(mdnAPI)
  .get(payload)
  .then(callback.success, callback.error);

// 메서드 호출을 실행하지만 프로미스 거부 경우를 다루는 다른 방법 (2)
$http(mdnAPI)
  .get(payload)
  .then(callback.success)
  .then(undefined, callback.error);



  var promise1 = new Promise(function (resolve, reject) {

    // 비동기를 표현하기 위해 setTimeout 함수를 사용
    window.setTimeout(function () {

        // 해결됨
        console.log("첫번째 Promise 완료");
        resolve("11111");

    }, Math.random() * 20000 + 1000);
});

var promise2 = new Promise(function (resolve, reject) {

    // 비동기를 표현하기 위해 setTimeout 함수를 사용
    window.setTimeout(function () {

        // 해결됨
        console.log("두번째 Promise 완료");
        resolve("222222");

    }, Math.random() * 10000 + 1000);
});


Promise.all([promise1, promise2]).then(function (values) {
    console.log("모두 완료됨", values);
});
```

## 참고 사이트

1. <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise>
2. <http://programmingsummaries.tistory.com/325>
