# Angular

## Atomic components

### View More

```ts
@Component({
  selector: 'viewmore',
  template: `<button (click)="onClick()">{{expanded ? 'View Less' : 'View More'}}</button>`,
})
export class ViewMoreComponent implements OnInit {
  @Input() limit: number;
  @Input() list: Array<any>;
  expanded: boolean = false;
  sliced;

  ngOnInit() {this.sliced = this.list.slice(0, this.limit);}
  onClick() {
    this.sliced = !this.expanded ? this.sliced = this.list : this.sliced = this.list.slice(0, this.limit);
    this.expanded = !this.expanded;
  }
}
```

usecase:
```html
<some-list *ngFor="let f of more.sliced" [file]="f"></some-list>
<viewmore #more [limit]="3" [list]="files"></viewmore>
```
templateRef sliced avoids using output, eventhandler, and storing lengths -> delegates that to the viewmore component