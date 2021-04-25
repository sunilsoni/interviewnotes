
Angular Pipes
==================

Angular Pipes are used to transform data on a template, without writing a boilerplate code in a component.

A pipe takes in data as input and transforms it to the desired output. It is like a filter in Angular 1 (AngularJS).

Generally, If we need to transform data, we write the code in the component, For example, we want to transform today’s date into a format like `'16 Apr 2018'` or `'16-04-2018'`
,We need to write separate code in the component.

So instead of writing separate boilerplate code, we can use the built-in pipe called `DatePipe` which will take input and transform it into the desired date format.

Syntax to use Pipes in Angular Application:
---------------
<img src="./images-pipes/anular-pipes.png" width="472" border="2" />

Types of Pipes in Angular:
---------------
The Angular Framework divided the Pipes into two types i.e. 
1. Built-in Pipes and 
2. Custom Pipes. 
   
Further Built-in Pipes are divided into two types i.e. Parameterized and chaining as shown in the below image.

<img src="./images-pipes/Types-of-Pipes.png" width="472" border="2" />

 1.Built-in Pipes
-----------------

Angular provides built-in pipes for typical data transformations, including transformations for internationalization (i18n), which use locale information to format data. The following are commonly used built-in pipes for data formatting:


[DatePipe](https://angular.io/api/common/DatePipe): Formats a date value according to locale rules.

[UpperCasePipe](https://angular.io/api/common/UpperCasePipe): Transforms text to all upper case.

[LowerCasePipe](https://angular.io/api/common/LowerCasePipe): Transforms text to all lower case.

[CurrencyPipe](https://angular.io/api/common/CurrencyPipe): Transforms a number to a currency string, formatted according to locale rules.

[DecimalPipe](https://angular.io/api/common/DecimalPipe): Transforms a number into a string with a decimal point, formatted according to locale rules.

[PercentPipe](https://angular.io/api/common/PercentPipe): Transforms a number to a percentage string, formatted according to locale rules.

For example,
```html
<table border="1">
    <thead>
        <tr>
            <th>Student ID</th>
            <th>Name</th>
            <th>DOB</th>
            <th>Gender</th>
            <th>CourseFee</th>            
        </tr>
    </thead>
    <tbody>
        <tr *ngFor='let student of students'>
            <td>{{student.ID | uppercase}}</td>
            <td>{{student.Name | titlecase}}</td>
            <td>{{student.DOB | date:'dd/MM/yyyy'}}</td>
            <td>{{student.Gender | lowercase}}</td>
            <td>{{student.CourseFee | currency:'USD':true}}</td>
        </tr>
    </tbody>
</table>
```

Output:

<img src="./images-pipes/student-table-output.png" width="472" border="2" />

 2.Custom Pipes
-----------------

To create a custom pipe, create a new ts file and use the code according to the work you have to do. You have to import Pipe, PipeTransform from Angular/Core. Let's create a sqrt custom pipe.


component.ts file:
```typescript
import {Pipe, PipeTransform} from '@angular/core';  
@Pipe ({  
name : 'sqrt'  
})  
export class SqrtPipe implements PipeTransform {  
transform(val : number) : number {  
return Math.sqrt(val);  
}  
}
```
Now, it's turn to make changes in the app.module.ts. Create a class named as SqrtPipe. This class will implement the PipeTransform. The transform method defined in the class will take argument as the number and will return the number after taking the square root.

As, we have created a new file so, we need to add the same in app.module.ts.

Module.ts file:
```typescript
import { BrowserModule } from '@angular/platform-browser';  
import { NgModule } from '@angular/core';  
import { AppComponent } from './app.component';  
import { NewCmpComponent } from './new-cmp/new-cmp.component';  
import { ChangeTextDirective } from './change-text.directive';  
import { SqrtPipe } from './app.sqrt';  
@NgModule({  
declarations: [  
SqrtPipe,  
AppComponent,  
NewCmpComponent,  
ChangeTextDirective  
],  
imports: [  
BrowserModule  
],  
providers: [],  
bootstrap: [AppComponent]  
})  
export class AppModule { }
```
Now, use sqrt pipe in component.html file.

component.html file:
```html
<h1>Example of Custom Pipe</h1>  
<h2>Square root of 625 is: {{625 | sqrt}}</h2><br/>  
<h2>Square root of 169 is: {{169 | sqrt}}</h2>  
```
Output:
```html
Example of Custom Pipe

Square root of 625 is: {{625 | sqrt}}

Square root of 169 is: {{169 | sqrt}}

```


For more information:
1. [Transforming Data Using Pipes](https://angular.io/guide/pipes)
2. [Angular Pipes](https://dotnettutorials.net/lesson/angular-pipes/)





