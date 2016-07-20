#Directive

Directive는 템플릿 구조를 모듈화하는 기능이라고 생각하면 쉽다.
간단한 예제를 통해서 Directive 맛만 보자.

```html
<ul ng-repeat="todo in todos | filter:statusFilter" class="list-unstyled">
  <li class="todo-item">

    <!-- 1. 이 부분이 하나의 todo 를 출력하는 부분이다. -->
    <div class="input-group">
      <span class="input-group-addon">
        <input type="checkbox" aria-label="..." ng-model="todo.completed">
      </span>
      <input type="text" class="form-control" aria-label="..." ng-model="todo.title">
      <div class="input-group-btn">
        <button class="btn btn-danger" ng-click="remove(todo.id)">Remove</button>
      </div>
    </div>

    <!-- 2. 위 코드를 아래 한 줄로 바꿔보자!!! Directive를 사용해서 -->
    <todo-item todo="todo" remove="remove(todo.id)"></todo-item>
  </li>
</ul>
```

`<todo-item>` directive를 만들겠다.

```javascript
angular.module('todomvc')
    .directive('todoItem', function (){
      return {
        restrict: 'E',
        scope: {        // 디렉티브 스코프 설정
          todo: '=',    // 양방향 바인딩
          remove: '&'   // 참고 바인딩. 함수 설정시 사용함
        },
        template:
        '<div class="input-group">' +
          '<span class="input-group-addon">' +
            '<input type="checkbox" aria-label="..." ng-model="todo.completed" ng-click="update(todo)">' +
          '</span>' +
          '<input type="text" class="form-control" aria-label="..."' +
            'ng-model="todo.title" ng-blur="update(todo)">' +
          '<div class="input-group-btn">' +
            '<button class="btn btn-danger" ng-click="remove(todo)">Remove</button>' +
          '</div>' +
        '</div>'
      }
    })
```
Directive를 정의 할때 `$scope`객체에 사용할 스코프 변수를 설정할 수 있다. `todo`는 데이터인데 출력과 수정을 해야하므로 양방향 바인딩 `=`을 사용했다. `remove`는 이벤트 핸들러 함수이므로 ckarhdyd `&`으로 사용했다.


##restrict 종류
값 | 설명           |
---|----------------|
`E`| Element name   |
`A`| Attrivute      |
`C`| Class          |
`M`| Comment(주석)  |

Default 값은 `EA`이다.


