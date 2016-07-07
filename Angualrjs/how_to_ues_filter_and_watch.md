#How to use filter & $watch

`ng-Repeat`는 기본적으로 필터기능을 지원한다. completed, active, all 세개 버튼을 만들어서 각각을 클릭할때 필터링 로직이 작동하도록 만들어 보자.

```html
<div class="btn-group" role="group" aria-label="...">
  <button type="button" ng-click="status='completed'">Completed</button>
  <button type="button" ng-click="status='active'">Active</button>
  <button type="button" ng-click="status=''">All</button>
</div>
```

어떤 버튼을 클릭했는지 상태를 저장하는 스코프변수 `$scope.status`에 저장한다.

필터에 따라 동적으로 `ng-repeat`가 동작해야 한다.
```html
<ul ng-repeat="todo in todos | filter:statusFilter"
```
버튼을 누를 때 마다 `statusFilter`값이 변할 것이다.


###$watch
이것은 스코프 변수의 변경을 감지하고 그때마다 사용자가 설정한 함수를 실행한다. (주의! 많이 사용하면 메모리 자원을 많이 먹는다.)

```javascript
// 필터버튼을 클릭하고 status 값이 변경되면 $watch()에 등록한 함수가 동작한다.
$scope.$watch('status', function () {
  if ($scope.status === 'completed') {        // Completed 클릭시
    $scope.statusFilter = {completed: true};  // 필터를 설정한다.
  } else if ($scope.status === 'active') {    // Active 클릭시
    $scope.statusFilter = {completed: false}; // 필터를 설정한다.
  } else {                                    // All 클릭시
    $scope.statusFilter = {};                 // 필터를 해제한다.
  }
})
```


