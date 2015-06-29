# controller-di
Inject controller dependencies into the controller instance

# What is controller-di?

Writing prototype based controllers with Angular is an efficient technique but quite tedious. 
All dependencies must be copied manually from the controller constructor to the controller instance. 
oc-controller-di allows you to specify the dependencies as usual and they will be automatically copied into the controller instance

## Installing

```javascript
bower install oc-controller-di
```

Add script references to oc-controller-di.js
Your html should look something like

```javascript
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" ng-app="MyApp">
<head>
    <title></title>
</head>
<body>
    <div ng-controller="HomeCtrl">
		<ul>
			<li ng-repeat="item in items">
				<span>{{item.name}}</span>
			</li>
		</ul>
    </div>

    <script src="angular.js"></script>
    <script src="oc-controller-di.js"></script>

    <script src="app.js"></script>
    <script src="HomeCtrl.js"></script>
</body>
</html>
```

Add module dependency. For example,

```javascript
angular.module("MyApp", ["ocControllerDI"]);
```

Now, inside the controller specify the dependencies as usual. For example,

```javascript
(function() {
	function HomeCtrl() {
		$scope.change = function () {
			setTimeout(function () {
				$scope.message = "XXX";
			}, 1000);
		}
	}
	
	HomeCtrl.prototype.refresh = function() {
		this.$http.get("/api/items").then(function(items){
			this.$scope.items = items;
		});
	}
	
	angular.module("MyApp").controller("HomeCtrl", ["$scope", "$http", HomeCtrl]);
})();
```

## See also
* [Eyal Vardi](https://eyalvardi.wordpress.com/2015/06/29/angularjs-tip-5-angularjs-arguments/#respond) - Original idea posted by Eyal Vardi