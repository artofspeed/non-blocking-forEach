# Non-blocking version of Array.forEach()

### What is it?
It creates a non-blocking version of .forEach(), allowing user’s browser to still be responsive as the loop runs in the background. This way, UX will be smoother and we avoid freezing the webpage when iterating over a large array that takes a shit load of time. Internally, it runs 1 iteration of the loop at each clock tick, instead of stacking iterations as much as possible.

### How to use
Simply copy paste the function below into your .js file
```
function asyncEach(items, fn, i){
    if (items.length <= 0) return;
    if (i >= items.length) return;
    if (!i) i = 0;
    fn(items[i]);
    setTimeout(function(){
        asyncEach(items, fn, ++i);
    }, 0);
}
```
### Example
This will print 1 2 3
```
asyncEach([1,2,3], function(n){
	console.log(n); 
});
```