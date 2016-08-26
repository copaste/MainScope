# MainScope
MainScope is an object, but it is not just an object, MainScope is a special object with some special features, which might be very usefull, when you want to detect changes in some objects. MainScope can listen for changes on its properties, this can be very helpfull in AngularJS, instead of using always $watcher that slows down the Application, you can use MainScope. You just have to attach a callback to the name of the property to which you want to listen. Let me give you simple example.

- The main disadvantage is that you should set your object structure in advanced.

```javascript
app.controller(['MainScope', function(MainsScope) {
  var ObjectILikeToListenOn = {
    filters: {
        age: null,
        sex: null,
        weight: null
    },
    sort: {
      byAge: null,
      bySex: null,
      byWeight: null
    }
  };

  this.scope = MainScope.addProp( 'filters', ObjectILikeToListenOn.filters );
  this.scope = MainScope.addProp( 'sort', ObjectILikeToListenOn.sort );
  
  // That is how we listen for changes on certain property
  this.scope.on('filters.age', function(newVal, oldVal, propMap, propName) {
    console.log(propMap, newVal, oldVal);
  });
  
  // That is how we listen for changes on certain object
  this.scope.on('sort', function(newVal, oldVal, propMap, propName) {
    console.log(propMap, propName, newVal, oldVal);
  });
  
  // That is how we remove a previously-attached event handler from cartain property.
  this.scope.off('filters.age');
}])
```

#Methods
```javascript
// Add new property to MainScope
MainScope.addProp('name', value );

// Atttach a callback: funciton (newValue, oldValue, propPath, propName)
MainScope.on('property.path', callback);
MainScope.on('property.path', funciton (newVal, oldVal, propPath, propName) {
  // - YOUR CODE GOES HERE - 
});

// Remove a previously-attached event handler
MainScope.off('property.path');

// Creates a new MainScope: 
MainScope.$new();
var newScope = MainScope.$new();
```

# License
MIT
