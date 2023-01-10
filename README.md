## Using Controllers Inside Directives
### Step 1: Declare Controller in Directive
```
function MyDirective(){
    var ddo = {
        scope: {
            prop: '='
        },
        controller: ControllerFunction,
        bindToController: true,
        controllerAs: 'myCtrl',
        templateUrl: "template.html"
    };
    return ddo;
}
```
`bindToController: true` - attach declared scope properties to controller instance instead of directly to $scope

`controllerAs: 'myCtrl'` - use 'myCtrl' in directive's template to refer to controller instance

### Step 2: Define Controller
```
ControllerFunction.$inject = ['Service'];
function ControllerFunction(Service){
    var myCtrl = this;
    myCtrl.method = function(){
        var name = "Hello " + myCtrl.prop;
        ...
    };
}
```
`var myCtrl = this;` - attach other properties to 'this' as usual

`myCtrl.prop` - use (& manipulate) props in isolate scope

### Step 3: Use In Directive's Template
```
<div ng-if="myCtrl.method()">
    {{myCtrl.prop}}
</div>
```
***
### One-way Binding
Watches only the identity of the parent property, not the property inside directive.
```
function MyDirective(){
    var ddo = {
        scope: {
            prop: '<'
        }
    };
    return ddo;
}
```
