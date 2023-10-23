---
description: >-
  Angular Pipes are a way to transform the view of data. It is a class with
  @Pipe decorator and implement `PipeTransform` interface. It accepts one or
  more input and return a transformed value
---

# \[Angular] Pipe

**Difference between pipe and impure  pipe**

Pure pipe will only be activated when the primitive value or the reference changes. Impure pipe, however, will be activated every time. Taking _clicking a button and add a value to an array_ as an example. Since it doesn't change the reference of an array, in the pure pipe, it will not immediately transform the view of data. Oh the other hand, the impure pipe will detect the change and re-render the view.&#x20;



#### To create a pipe, create a .pipe.ts file with @pipe decorator

{% code title="search.pipe.ts" %}
```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
name: 'search'
})
// the pipe class is decorated with @pipe, and implement the `transform` function
export class SearchPipe implements PipeTransform {

transform(value: any, name: string) {
	if(name === ''){
	return value;
	}
	return value.filter((employee) => {
	employee.firstName.startsWith(name)
});
}
}
```
{% endcode %}

#### **Then you can register the pipe in your component like this**

```html
<div class="container">
<h1>Employee Details</h1>
<span>Search </span>
<input type="text" [(ngModel)]="nameString">
<br/><br/>
<table class="table table-sm table-striped m-t-4">
	<thead class="thead-dark">
	<tr>
	<th>First Name</th>
	<th>Last Name</th>
	<th>Department</th>
	<th>Salary</th>
	<th>Joining Date</th>
	</tr>
</thead>
<tbody>
	<tr *ngFor="let employee of employees | search:nameString">
	<td>{{employee.firstName}}</td>
	<td>{{employee.lastName}}</td>
	<td>{{employee.dept}}</td>
	<td>{{employee.salary | currency}}</td>
	<td>{{employee.doj | date:'dd/MM/yyyy'}}</td>
	</tr>
</tbody>
</table>
<button type="button" class="btn btn-success m-3"
		(click)="addUser()">
	Add Employee
</button>
<button type="button" class="btn btn-success"
		(click)="reset()">
	Reset
</button>
</div>
```





**Conclusion:**

* Pure pipes detect changes only when there is a change to primitive types or object reference.&#x20;
* Pure pipes optimize the angular change detection cycle because checking primitive values or object references is much faster than detecting a change within an object.&#x20;
* It is better to avoid impure pipe since it could be a great hindrance for performance due to the excessive and heavy change detection.



**Reference**

[Explain pure and impure pipe in Angular](https://www.geeksforgeeks.org/explain-pure-and-impure-pipe-in-angular/)

