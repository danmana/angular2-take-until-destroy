# Angular 2 - easy unsubscribe when component destroyed 

##### Angular 2 decorator - easy and declarative way to unsubscribe from observables when the component destroyed

## Installation
`npm install angular2-take-until-destroy --save`

## Usage
```js
import TakeUntilDestroy from "angular2-take-until-destroy";

@Component({
  selector: 'app-inbox',
  templateUrl: './inbox.component.html'
})
@TakeUntilDestroy
export class InboxComponent {
  componentDestroy;
  constructor( ) {
    const timer$ = Observable.interval(1000)
      .takeUntil(this.componentDestroy())
      .subscribe(val => console.log(val))
  }

  // This method must be present, even if empty! 
  // Otherwise 'ng build --prod' will optimize away any calls to ngOnDestroy, 
  // even if the method is added by the @TakeUntilDestroy decorator
  ngOnDestroy() {
    // You can also do whatever you need here
  }

}
```

