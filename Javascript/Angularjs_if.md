#AngularJS 조건문

AngularJS의 조건문은 4가지가 존재한다.

- ng-switch
- ng-hide, ng-show
- ng-class
- ng-if

##1. ng-switch

```html
<div ng-switch on="fruits">
    <div ng-switch-when="apple">
        <!-- fruits값이 apple일 때 해당 태그가 실행됩니다.-->
    </div>
    <div ng-switch-default>
        <!-- code to render the regular video block -->
    </div>
</div>
```
`on`에 `switch`의 대상이 되는 변수를 적어준다.

###ng-switch 예제
```html
<div ng-app="">
	<input type="text" ng-model="fruits">
	<p>입력한 값: {{Var}}</p>
	<div ng-switch="" on="fruits">
		<div ng-switch-when="appel">
			apple을 입력!
		</div>
		<div ng-switch-default>
			아무것도 입력하지 않음
		</div>
	</div>
</div>
```

##2. ng-hide / ng-show

```html
<div ng-hide="isBlockedMember">
    <!-- isBlockedMember가 true값을 가지면 해당 <div>태그는 보이지 않습니다.-->
</div>
<div ng-show="isLogged">
    <!-- isLogged가 true값을 가지면 해당 <div>가 보이게 됩니다. -->
</div>
```

특정 조건에 있어 show/hide를 할 수 있는 `directive` 이다.

###ng-hide / ng-show 예제
```html
<div>
	<spand>isMember:</span>
	<select ng-model="isMember">
		<option value="true">YES</option>
		<option value="false">NO</option>
	</select>
	
	<p>isMember : {{isMember}}</p>
	<div ng-show="isMember=='true'">
		회원입니다.
	</div>
	<div ng-hide="!(isMember=='false')">
		회원이 아닙니다.
	</div>
</div>
```

##3. ng-class

```html
<div ng-class="{block-member: member.isBlocked}">
    <!-- member객체의 isBlocked의 값이 true이면 해당 태그에 block-member클래스가 등록됩니다. -->
</div>
```
css와 함께 태그를 컨트롤하기에 좋음

###ng-class 예제

```html
<div style="width:100%; background-color:#eee">
	<span>chang Background color: </span>
	<input type="text" ng-model="bgColor" placeholder="red를 입력해보세요.">
	<div style="width:200px; height:100px;" ng-class="{'red: bgColor=='red'}">
	</div>
</div>
```

##4. ng-if

```html
<div ng-if="lastLogged == today">
    <!-- 변수의 값이 today와 일치할 때 이 태그가 보여지게 됩니다.-->
</div>
<div ng-if="lastLogged != today">
    <!-- 변수의 값이 today와 일치하지 않을 때 이 태그가 보여지게 됩니다. -->
</div>
```

`ng-else`는 존재하지 않는다!!

--
###Reference
- [고무망치](http://rhammer.tistory.com/55)
- [angularJs](https://www.angularjs.org)