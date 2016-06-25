# retry
###signature: `retry(number: number): Observable`
*The gist: Retry specified number of times on error...*

([jsBin](http://jsbin.com/yovacuxuqa/1/edit?js,console) | [jsFiddle](https://jsfiddle.net/qg6qfqLz/11/) | [ official docs](http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html#instance-method-retry))
```js
//emit value every 1s
const source = Rx.Observable.interval(1000);
const example = source
  .flatMap(val => {
    //throw error for demonstration
    if(val > 5){
      return Rx.Observable.throw('Error!');
    }
    return Rx.Observable.of(val);
  })
  //retry 2 times on error
  .retry(2);
/*
  output: 
  0..1..2..3..4..5..
  0..1..2..3..4..5..
  0..1..2..3..4..5..
  "Error!: Retried 2 times then quit!"
*/
const subscribe = example
  .subscribe({
     next: val => console.log(val),
     error: val => console.log(`${val}: Retried 2 times then quit!`)
});
```