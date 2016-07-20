#Promise객체 와 $q서비스

##Promise객체
promise 객체는 약속을 표현하는 자바스크립트 객체이다.

AngularJS에서 `$http`,`$tiemoute`,`$resource`,`$route`등 여러 서비스에서 promise객체를 반환한다.

```javascript
function fetchData(id, cb){
  getDataFromServer(id, function(err, result){
    if(err){
      cb(err, null);
    }else{
      transformData(result, function(err, transformedResult){
        if(err){
          cb(err, null);
        }else{
          saveToIndexDB(result, function(err, savedData){
            cb(err, savedData);
          });
        }
      });
    }
  });
}
```
위 코드는 콜백지옥이다. promise객체를 사용하면 다음과 같다.

```javascript
function fetchData(id){
  return getDataFromServer(id)
          .then(transformData)
          .then(saveToIndexDB);
}
```
then으로 묶어 주면 된다. 코드가 예뻐졌다. 그리고 `error`처리도 쉬워진다.

```javascript
fetchData(1)
  .then(function(result){

  }, function(error){
    // exceptions in transformData, or saveToIndexDB
    // will result in this error callback being called.
  });
```

##Deferred객체
약속을 정의했으면 누군가는 약속을 지키거나 거절해야 한다. 이러한 일을 하는 것이 `deferred`객체이다. `deferred`객체는 약속을 만들고 만든 약속의 상태를 변경한다.

AngluarJS는 `$q.deferred()`를 이용하여 `deferred`객체를 생성할 수 있다. (`deferred`객체 생성은 곧 `Promise`객체 생성이기도 하다.)

`deferred`객체는 `resolve`,`reject`,`notify`를 통하여 약속으 지키거나 거절/취소하여 진행 상태를 알려준다.


`deferred`객체는 주로 별도의 서비스를 만들고 해당 서비스에서 생성하여 해당 객체의 약속을 반환하는 식으로 많이 사용된다.

```javascript
angular.module('demo-app', [])
  .factory('userService', function($http, $log, $q) {
    return {
     getUser: function(userId) {
       //deferred 객체를 생성한다.
       var deferred = $q.defer();
       $http.get('/api/users/' + userID)
         .success(function(data) { 
            //요청이 성공하면 약속을 지키고 별도 데이터를 전달한다.
            deferred.resolve({
               name: data.name,
               address: data.address});
         }).error(function(msg, code) {
            //요청이 실패하면 약속을 취소하고 메시지를 전달한다.
            deferred.reject(msg);
            $log.error(msg, code);
         });
       //해당 deferred 객체의 약속을 반환한다.
       return deferred.promise;
     }
    }
	});
```

##여러 Promise 묶어주기($q.all)
$q 서비스는 미래에 지켜지거나 지켜지지 않을 여러 약속을 하나의 약속으로 처리할 수 있는 API도 제공한다. 

```javascript
factory('asyncService', function($http, $q) {
  return {
    loadDataFromTwoReq: function() {
      var deferred = $q.defer(),
          httpPromise1 = $http.get('/api/req1'),
          httpPromise2 = $http.get('/api/req2');

      //두 약속을 $q.all 메서드를 이용해 새로운 약속을 만든다.
      $q.all(httpPromise1, httpPromise2)
        .then(
          function(results) {
            //두 약속이 모두 지켜지면 asyncService서비스가 반한하는 약속을 지키고 두 약속이 전달하는 결과를 묶은 배열로 전달한다.
            deferred.resolve(results) 
          },
          function(errors) {
            deferred.reject(errors);
          },
          function(updates) {
          deferred.update(updates);
        });
      return deferred.promise;
    }
  };
});
```

위 코드는 일반적인 콜백 방식으로 작성하게 되면 첫 번째 요청의 성공 콜백에서 다른 요청을 하고 그 요청의 성공 콜백에서 두 요청에 대한 성공 처리를 하는 코드를 작성하게 된다. 

하지만!! $q 서비스는 $q.all 메서드를 이용해 약속을 바환하는 여러 비동기적인 일이 병렬적으로 행해지고 있다.
약속을 하나로 묶어 성공/실패 처리를 할 수 있게 해준다.




###References
- [시작하세요! AngularJS프로그래밍](http://wikibook.co.kr/beginning-angularjs/)
- [Promises in AngularJS, Explained as a Cartoon](http://andyshora.com/promises-angularjs-explained-as-cartoon.html)
- [angularjs official document](https://docs.angularjs.org/api)


  
  