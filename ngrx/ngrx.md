# NgRx

## Reducers

### Multiple Actions that to do same thing
```ts
export function bugerReducer(state, action) {
    switch (action.type) {
        case '[Menu Page] Add burger':
        case '[Burger Details Page] Add burger':
            return {...state, action.burger};
        default:
            return state;
    }
}
```

## Effects


### Same Effect triggered by mulitple Actions

```ts
addBurger$: Observable<any> = this.actions$
.ofType('[Menu Page] Add burger', '[Burger Details Page] Add burger')
.switchMap(...)
```

### Dispatch mulitple Actions from effect
```ts
removeBurger$: Observable<any> = this.actions$
.ofType('[Menu Page] Add burger')
.switchMap((action: menuActions.AddBurger | details.AddBurger) => {
    const p = action.payload;
    return this.burgerService.addBurger(p.id)
    .mergeMap(res => [
        new burgers.Load(), // refresh burger list
        new burgers.BurgerAddSuccess('Burger was successfully added.')
    ])
    .catch(err => {
        return of(new tasks.DeleteTaskFail(err.statusCode));
    });
}))
```