# controller-di
Inject controller dependencies into the controller instance

# What is controller-di?

Writing prototype based controllers with Angular is an efficient technique but quite tedious. <br/>
All dependencies must be copied manually from the controller constructor to the controller instance. <br/><br/>
<strong>oc-controller-di</strong> allows you to specify the dependencies as usual and they will be automatically copied into the controller instance <br/>

## Installing

```javascript
bower install oc-controller-di
```

Add script references to <strong>oc-controller-di.js</strong><br/>
Your html should look something like

```javascript
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" ng-app="MyApp">
<head>
    <title></title>
</head>
<body>
    <div ng-controller="HomeCtrl as ctrl">
		<ul>
			<li ng-repeat="item in ctrl.items">
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
	//
	//	$scope and $http will be injected automatically into the controller instance before the constructor is invoked
	//
	angular.module("MyApp").controller("HomeCtrl", ["$scope", "$http", HomeCtrl]);
	
	function HomeCtrl() {
		//
		//	Additional fields (beside those that are injected automatically)
		//
		this.items = [];
	}
	
	HomeCtrl.prototype.refresh = function() {
		var me = this;
		
		this.$http.get("/api/items").then(function(items){
			me.items = items;
		});
	}	
})();
```

## See also
* [Eyal Vardi](https://eyalvardi.wordpress.com/2015/06/29/angularjs-tip-5-angularjs-arguments/#respond) - Original idea posted by Eyal Vardi