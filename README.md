# Materials

Angular 7 Handy Notes 
=======================
Angular is a javascript framework which allows u to create a reactive single page apps

git clone https://github.com/angular/quickstart Demo 

How to Create Angular project From Angualar CLI 

Angular Organises a code in a clean Structural

Easy to test
makes development easier



Building Blocks of Angular Apps
================================

Component 
Directive
Service
Module
Filter
D.I
Bindings
Pipes

What is a Component :
These are the basic building blocks of angular application to control HTML views.
The Angular components encapsulates template, data and a behavior of a view. In simple words Angular components are nothing but a typescript class with some metadata attached to it(with the use of decorator Angular).

Lets understand this with an example:

Consider your webpage with a navigation bar at the top and a sidebar menu. For this webpage design you can create 2 components for navigation bar and side bar respectively. Let us see navbar component :

import { Component } from '@angular/core'; 
 
@Component({ 
selector: 'nav-bar-component', 
template: `<div class="navBarContainer">
	<ul (click)="hideNavList()">
		<li>tabsData[0]</li>
		<li>tabsData[1]</li>
		<li>tabsData[2]</li>
	</ul>
</div>`
}) 
 
export class NavBarComponent{ 
	tabsData = ["Home","Contact Us","About Us"];
	constructor() {}
 
	hideNavList() {
		//code to hide the list 
	}
}

Here as you can see in navbar component you have defined your template using unordered list. Also you have provided tabsData as a data to bind to the template and hideNavList() as behavior to the view. Likewise you can create the other components in Angular.

###########################################  OR  ######################################################################################################

 

Components are basic building blocks of an Angular application
Component it encapsulates the data,html mark up,logic for a view whcih an area of a sceen an user can see it .
To create a component in Angular with TypeScript, create a class and decorate it with the Component decorator.
Consider the sample below:

import { Component } from '@angular/core';
@Component({
  selector: 'hello-ng-world',
  template: `<h1>Hello Angular world</h1>`
})
export class HelloWorld { 
}
Component is imported from the core angular package. The component decorator allows specifying metadata for the given component. While there are many metadata fields that we can use, here are some important ones:

selector: is the name given to identify a component. In the sample we just saw, hello-ng-world is used to refer to the component in another template or HTML code.
If you put there .hello-ng-world then you get <div class="hello-ng-world"></div>. You can even use [hello-ng-world] to look for properties. (like <div hello-ng-world></div>).

template: is the markup for the given component. While the component is utilized, bindings with variables in the component class, styling and presentation logic are applied.
templateUrl: is the url to an external file containing a template for the view. For better code organization, template could be moved to a separate file and the path could be specified as a value for templateUrl.
styles: is used to specific styles for the given component. They are scoped to the component.
styleUrls: defines the CSS files containing the style for the component. We can specify one or more CSS files in an array. 
From these CSS files, classes and other styles could be applied in the template for the component.


Component in Action :
=====================
create a component 
Register that component to the module
Add an element to a Html markup (VIA selector)

 ng new project-name
 or 
 ng init project-name
 
 To create a component using Angular CLI
 ng generate component navbar
 
 ng g c about
 ng g c contact
 ng g c home
 
A Module is a container for a group of related compoments 

Bindings 
============
1)Property Binding  : we bind the property of a dom element to a field  in component  
======================
it works with  only one way binding 

Ex :
====

<img src ="{{imageValue}}" > My Image </img>
 (or)
<img [src] ="imageValue" > My Image </img>

Interpolatoin : {{component field }}
{{Title}} ----> String Interpolatoin
    (or)
<h2  [textContent]="title">  -------> Property binding 




2)attribute bindings
==================
Binding an Attribute of Html element into component field 

colspan is an html td attribute doesn't have a dom property as colspan so we are using [attr.colspan] 
<td colspan="2" > </td>    --------> <td [attr.colspan]="2" >

Class Binding 

<button class="btn btn-primary"  [class.active]={isActive}>

based on some condition we want to add active class dynamically  


Style binding 


<button [style.background] = "isActive ? 'blue' : 'white'}">



Event Binding  which we used to handle event raised by dom like Button click,mouse over,mouseout,keyup etc ...


* () used for  ----> For Event Binding 

Bind this as a method on a component

<button (click)="onSave();"> Save  </button>\

Event Filtering 
===============

in template 
<input (keyup) =onKeyup() />

in componet

onKeyup($event)
{

 if($event.code =="13")
{
console.log("enter key was pressed")
}
}

(or) 
<input (keyup.enter) =onKeyup() />
in componet

onKeyup()
{
	console.log("enter key was pressed")

}

***************************************************************************************************************************************************************************

Template  Variable
*********
email
i)  event.target.value gives the value entered in input field
       (or )
ii) template :   ~
								< input #email (keyup.enter) =onKeyup(value) />
			     ~

	onKeyup(email)
	{
		console.log(email);
	}

	
	
***************************************************************************************************************************************************************************
	
	2 way binding :
	
	===========================
					1 way binding example 
					
					<input [value] ="email" (keyup.enter)="onKeyup();"

					Component.ts : 
					email :String="phanindra1212@gmail.com";
					onkeyup()
					{
					   console.log(this.email);
					}

	2 way binding : Approach 1:
	
	template : ~
				<input [value] ="email" (keyup.enter)="email =$event.target.value=onKeyup()"
		2 way binding : Approach 2:
			     <input [(ngModel)] ="email" (keyup.enter)="onKeyup()" />
	
	
			~
			
	Component :
	==========

  export class eventComponent
  email="me@example.com"
  
  onKeyup()
  {
    console.log(this.email);
  }
  
  ngModel we need to excliptly import 
  
  
  
  		
	Component :
	==========
  
  
  
  
  
  
  Pipes :Pipes are used to format the data
  bultin pipes lowercase,uppercase,currency,Date etc 
  For LowerCase or UpperCase
	EX:
	===================================================================================
	{{courses.title | uppercase|lowercase}}
	{{courses.students | number}}
	{{ courses.rating | number : '2.2-2' }}
	{{ courses.price | currency}}
	{{ courses.price | currency:'AUD'}}
	{{ courses.price | currency:'AUD':true:3.2-2}}
	{{courses.date | date:shortDate }}
	

	Component																					Directive
	============																			=============================
To register a component we use @Component meta-data annotation	                    To register directives we use @Directive meta-data annotation
Components are typically used to create UI widgets	                                Directive is used to add behavior to an existing DOM element
Component is used to break up the application into smaller components				Directive is use to design re-usable components
Only one component can be present per DOM element									Many directives can be used per DOM element
@View decorator or templateurl/template are mandatory								Directive doesn't use View

	
	
	
	
  
  Reusable Components :we use i/p and o/p properties to make reusable compoments 
  
  Input Properties
  ===============
  to pass input or state to a component 
  
  We Can Use @Input Decorator to bind our favourite component value availble to app.component.html to use @ input() decorator we need to import 
  or 
  2nd apporach 
  
  we can define in component i,e Component : 'inputs'  :[isfavourite]
 
  OutPut Properties 
  ===============
  to raise a event from this custom component
  public api is a combination of both i/p properties and o/p properties .
 
 
 
 143610
 
 
 
 Component	Directive
To register a component we use @Component meta-data annotation	To register directives we use @Directive meta-data annotation
Components are typically used to create UI widgets	Directive is used to add behavior to an existing DOM element
Component is used to break up the application into smaller components	Directive is use to design re-usable components
Only one component can be present per DOM element	Many directives can be used per DOM element
@View decorator or templateurl/template are mandatory	Directive doesn't use View

 
 
 Directives :are used to modify the dom 
 Directives add behaviour to an existing DOM element or an existing component instance.


      (or) 
 used to attach a special behaviur to DOM 
 2 types 
 
 Structural Directive :Modify the structure of the Dom element by adding /removing Dom 
 
 Attribute Directive : Modify the attributes of the Dom element 
 
 Ng- IF :Before Angular 4
 ========
 
 in App-component.html
 
 
 <div *ngif="courses.length>0">
  Courses List
 </div>
 
 
 
 <div *ngif="courses.length ==0">
    No Courses Availble

 </div>
 
 
 ex 2)
 
 <div *ngIf="courses.length>0 ; else noCourses">
			Courses List
 </div>
 
 
  
 <ng-template #noCourses>
		No Courses Availble
  </ng-template>
 
 
 ex 3)
 
 <div *ngIf="courses.length>0 ; then CoursesList else noCourses">
			Courses List
 </div>
 
 <ng-template #CoursesList >
		 Courses List
  </ng-template>
  
 <ng-template #noCourses>
		No Courses Availble
  </ng-template>
 
 
 To Show/Hide Part of a page
 instead of using ngIf Directive we can use hidden attribute
		 
		 <div [Hidden] ="courses.length==0">
		  Courses List
		 </div>
		 
 
 
	 <div [Hidden] ="courses.length >=0">
		No Courses Availble

	 </div>
	 
	 Diff between ng-IF Directive & Hidden Attribute
	 in ng-If   if condition is true that elements will be added to Dom
	 but in attribute both are availble in dom
	 
	 Ng-SwithCase 
	 if you want to compare the value of field or property in its multiple values 
	 
	 Ng-For 
	 used for render list of objects 
	 
	 *ngIF:
	 
	 
	 
	 What is a module?
Modules are logical boundaries in your application and the application is divided into separate modules to separate the functionality of your application. Lets take an example of app.module.ts root module declared with @NgModule decorator as below,

import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';

@NgModule ({
   imports:      [ BrowserModule ],
   declarations: [ AppComponent ],
   bootstrap:    [ AppComponent ]
})
export class AppModule { }
The NgModule decorator has three options

The imports option is used to import other dependent modules. The BrowserModule is required by default for any web based angular application
The declarations option is used to define components in the respective module
The bootstrap option tells Angular which Component to bootstrap in the application


	 
	 Forms 
	 
	 Form Control:
	 Form Group:  

	 Types of Forms 
	 Template Driven
	 Reactive Forms 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 Routing:
	 
	 3 Steps
	 
	 Configure Route :
	 Add RouterOutLet
	 Add Links routerLink=""
     routerLinkActive

 Promise: The definition
  A Promise is an object representing the eventual completion or failure of an asynchronous operation. 
  Essentially, a promise is a returned object you attach callbacks to, instead of passing callbacks into a function.

Promise: In Layman terms
Think of it as a conversation between two people:

Alex: Hey Mr.Promise! Can you run to the store down the street and get me itemA for this dish we are cooking tonight?
Mr. Promise: Sure thing!
Alex: While you are doing that, I will prepare itemB(asynchronous operation). But make sure you let me know whether you could find itemA (promise return value).
Mr. Promise: What if you are not at home when I am back?
Alex: In that case, send me a text message saying you are back and have the item for me (success callback). 
If you don’t find it, call me immediately (failure callback).
Mr. Promise: Sounds good! See you in a bit.
So simply speaking, promiseobject is data returned by asynchronous function. It can be a resolveif the function returned successfully or a rejectif function returned an error.


var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});
The promise constructor takes in one argument: a callback function with two parameters — resolve and reject. This promise can then be used like this:

promise.then(function(result) {
  console.log("Promise worked");
}, function(err) {
  console.log("Something broke");
});
If promise was successful, a resolve will happen and the console will log Promise worked, otherwiseSomething broke. That state between resolve and reject where a response hasn’t been received is pending state. In short, there are 3 states to a promise:

pending: awaiting promise response
resolve : promise has successfully returned
reject: failure occurred



    //Open a new XHR
    var request = new XMLHttpRequest();
    request.open('GET', url);

    // When the request loads, check whether it was successful
    request.onload = function() {
      if (request.status === 200) {
        // If successful, resolve the promise
        resolve(request.response);
      } else {
        // Otherwise, reject the promise
        reject(Error('An error occurred while loading image. error code:' + request.statusText));
      }
    };

    request.send();
  });

};

const embedImage = url => {
  loadImage(url).then(function(result) {
      const img = new Image();
      var imageURL = window.URL.createObjectURL(result);
      img.src = imageURL;
      document.querySelector('body').appendChild(img);
    },
    function(err) {
      console.log(err);
    });
}


An observable acts as a container for an item or collection of items.
These items in the container are not stored in memory, rather the items are added in asynchronous fashion (like events).
Now, whenever the observer 	, he or she can be able to access the items in the observable.
Later the observer can be able to manipulate the received items.













Unit Testing 

Test a component in a isolation without an external resource (eg file system ,database,Api End Points)


Integration Test 

Test a component  with an external resource (eg file system ,database,Api End Points)


End to End Test :

Test the entire application as whole 










let promise = new Promise(function(resolve, reject) {
  resolve("done");

  reject(new Error("…")); // ignored
  setTimeout(() => resolve("…")); // ignored
});

