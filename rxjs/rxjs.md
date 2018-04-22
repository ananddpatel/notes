# RxJs

## Operators

### mergeMap
*http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-mergeMap*

```mergeMap()```merges the letters into the inner Obvervable ```results``` so that the value by the value emitted after the interval contains all 3 elements from ```letters```

```js
let letters = Rx.Observable.of('a', 'b', 'c');
let result = letters.mergeMap(x =>
  Rx.Observable.interval(1000).map(i => x+i)
);
result.subscribe(x => console.log(x));

// Results in the following:
// a0
// b0
// c0
// a1
// b1
// c1
// a2
// b2
// c2
// continues to list a,b,c with respective ascending integers
```

### switchMap
*http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-switchMap*

```switchMap()``` will unsubscribe from the Observable returned by ```project``` as soon as it has invoked it again on a new element. The marble diagram indicates this with the missing third 30 item in the output Observable

```js
let letters = Rx.Observable.of('a', 'b', 'c');
let result = letters.switchMap(x =>
  Rx.Observable.interval(1000).map(i => x+i)
);
result.subscribe(x => console.log(x));

// Results in the following:
// c0
// c1
// c2
// ...
```