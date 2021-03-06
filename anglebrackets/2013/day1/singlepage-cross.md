# 0 to 60 with Single Page Apps & HTML5

Presentors: 

* John Papa (@john_papa)
* Ward Bell (@wardbell)

## Vanilla JS

A javascript framework that is one every single device that exists today!  If you just went *what*, let me explain what vanilla js is.  Vanilla js is the javascript language itself, or js out of the box.  Make sure that what you are doing actually needs a framework, because you can do a lot with out of the box javascript.

## SPAs

Definition: single page application.  Presentor is going to use angularjs as the spa framework for today.  Don't mix frameworks, pick one and stick with it.  Mixing spa frameworks is just asking for a jumbled mess!

Questions that you should ask when choosing a framework:

* What do I need?
* What options do I have?
* What do I need to know?
* What can I build?

If you can't get approval to turn your entire app into spa, just know that you can just do a small section as a spa.  Just phase in the spa, slowly taking in more and more pages that the spa handles.

## What do we want in a SPA framework

When the presentor codes he likes to write things that are single responsibility, so he also wants his framework to be written in this way also!

Apps should be written in small files, while each file handles one thing.  Each one names with what it handles.

Your SPA framework should make writing applications in this way easy.  The framework should contain **Routing** and **DI**.

With DI the framework will handle loading the files and the dependances that you will need to use in each class.

Routing is an absolute must have.  While the name of the presentation is Single page, you will be writing many views that are shown from this one page.  Routing handles moving from view to view, back and forth.

Data binding, how to keep the view up to date with models that are changing over time.  Do you have to refresh the whole screen. Do you have to manage how you display each model and keeping it up to date. NO, your framework should handle that.

Along with data binding, the framework should handle all the DOM monipulation.  DOM monipulation is the most expensive thing that you will do in the browser.  Let the framework handle this, so that you dont have to worry about destroying the browser.

How does the framework manage DOM manipulation?  DOM Templates should come standard with your framework.  You should only have to define how to display a model once and have that template be used everywhere.  Coming alon with this is **Views**.  You should not have to re-write the same bit of views over and over accross your application if they are all the same.  The framework should allow you to re-use views easily across the site.

* DI
* Routing
* MV*
* Data Binding
* DOM Templates
* Views

If you think there are some things missing in this list, you would be correct.  A SPA framework is a presentation framework.  It does not need to handle every thing, that is the idea behind single responsibility. You will need to load data from your server, handle security, and other things that are not related to the presnetation.

## Value of Presentation frameworks

* Reduces the Plumbing
 * There are a lot of things that have already been solved.  Let people who specalize in these things write the specialty code
* Handles the 
* TODO

## Conventional asp.net app

broswer client, html + jquery
Server: presentation, business logic, data access
Database

---

smart client
Desktop client, presentation ui logic, data access
server service
database

---

single page applications
browser: presentation html/css, ui logic, data service access
service: service content service
database

---

People who switched over to smart clients, have been using these concepts for quite a while.  How you do this on the client is pretty much the same, just without plugins and just using the browser.  Same architecture ... different technology

## SPA Features (Presentation FrameWorks)

* Orgnization
* Page LifeCycle
* Dependency Mgt
* MV*
* Routing
* UI Interaction
* Data Binding
* Services

What is ** NOT **

* Rich Data
* UI Controls
* Testing
* CSS / Styling
* Your Logic :)
* Security

Picking which SPA framework based off of the Todo app example. hahahah.  It is not for deciding, but ot see how the framework style looks. Ask **WHY** 5 times before you make any decisions.

A presenstion framework should do presentation well.  jQuery and other frameworks in js are just doing way to much so that puts them in a position where they give you the kitchen sink, but that isnk is not the best.

## Data Binding

With angularjs, your databinding is just {{variable}} with in the html. there is no <%= variable %>.  You should not have to write so much.

When working with attributes that are on html elements, always start with data-.  You techinically do not have too, but in html5 it is a reserved attribute name that does not slow down the browser from trying to see if it understands what you are saying.

## MV*

How to you attached you html to you model to your view. No javascript in the view, an dnot html in the viewModel.  With Angular you should not have to mix these two items.  Putting this information in each, it makes reading and understanding in the long term very hard.  What should the screen present is the view.  The actual data that the needs to be updated or seen is the ViewModel.

Putting you View without having js mixed it, it allows you to make sure that you html is valid.  Putting a view together by appending strings on strings, how do you know that you are writting valid html?  Browsers and other things have been built to do things really well, when you mix js and html you are saying that you dont care that they do it better.

## Dynamic View Composition

View do not have to have everything in them.  Your views should also handle one thing and one thing only.  use views inside of views inside of views.  Then you only have to worry about exactly what you are trying to view in one html file, not everything in one html file.

# AngularJs

Getting angularJs is as easy as doing a nuget package in .Net.  You can also download the framework from the [Angularjs website](http://angularjs.com).  Presentor says that you should install the latest unstable version that is in rc3, so it is not really that unstable.  The big thing in the new version is that all the different services and extras are now in specific modules that are in seperate js files.  You can decide what you need, not just everything.  Recomended starting modules: Core, Route, Animate.

``` install-Package angularjs.core -pre ```

Why the pre?  Since this uses a rc3 nuget says that it should be a prerelease, not a full release.

## Lets write a quick app

*NOTE: For most of us, putting the script tags at the end of the body is nothing new.  if that is new to you, I would very much recommend following this standard.*

Two-way data binding and One-way data binding are done in different ways.  What is the difference between two-way and one-way?  One-way will keep the ui up-to-date as he model changes. Two-way keeps the model up to date as he user puts some input into the form and then also keeps the ui up to date as the model changes.  One-way binding can be done with {{variable}} or as a ng-bind attribute.  Two-way is always done as an attribute ng-model.

Why would I do a mustache (*{{variable}}*) compared to ng-bind?  Well the only time that you should really use the attribute version is on the page that is initially loaded when the browser starts up.  Thiswill keep the user from seeing mustaches as teh javascript loads. If you do the mustache for a split second, or however long it takes to load angularjs on teh browswer, the user will see he mustache on the page.

### DI

How does angularjs handle di?  when you define a modeule there is an array of modules names that is taken in as the second param.  This array is a list of strings of module names that your module you are creating releys on.

```js
var myModule = angular.module('myModule', 
	['ng-route','ng-locale', 
	function(route,locale){
		//module code
	}); 
```

## Coding conventions of Presentor

When defining a controller, he likes to define all the things that he will define too.  it is very similar to doing the properties at the top of a class.  Even for functions that you are going to make available to the outside world, add the variable pointing to the function at the top.  Don't write the function inline, the point of puting all this stuff at top is to make everything glancable.  If everything is defined inline then there will be a lot of scrolling just to glance at what is available to bind against.

Another thing he likes to do is assign this to vm right at the begining.  This gives it more semantical meaning then that and this and me.  This also removes the scoping out issue of this, which gets a lot of people.

```js
var myModule = angualar.module('myModule', function(){
	var vm = this;
	
	vm.save = save;
	
	fucntion save(){
	// code for save
	};
});
```

## AngularJs Triangle (Directives)

Html is nothing but html.  ViewModels are just js with data.  If you need these two to come together, it is a directive.  Directives will handle creating html for js code.  This is the only place in your code where html and js should play together or know about the other.

Presentor tip, before you create a directive (custom) always make sure that you look at the angularjs docs.  A lot of the time what you are looking for is already in the framework, if it is a common task.  Some examples are dblClick, Click, Blur, etc..

## AngularJs Controllers

Be consistant with how you do controller definitions.  There are a number of ways to do controllers, keeping your team all doing the samething will save a bunch of headaches.  A good way to keep your team to always do thing the same way is to use [SideWaffle](http://sidewaffle.com/).

## AngularJs Dependancies For Controllers

When adding a controller to a module, the signaure is controller name, controller constructor.  But there is a special way that you can pass in the constructor where you can specify what angular needs to pass into your constructor as dependancies.  If you pass teh constructor parameter as an array, where the first elements are strings that match the exact name of dependancy as it was defined on the module.  Then the last parameter is the actual constructor function with a signature that matches he previous elements in the array and in the same order.

```js
var myController = angular.app('myApp')
	.controller('myController', ['myExactDependancyName', 'myOtherExactDependancyname',myControllerConstructor]);

function myControllerConstructor(dependancy, otherDependancy){
};
```

Notice how the string in the array is an exact name, but in the signature for the controller they are just what ever I want the variable to be named.  Array name must be exact, constructor signature just has to be in the same order as the array but can be any names.

## Setup AngularJs App a runtime

Configuring the routes that your app supports:

```js
app.config([]);
```

If there is some code you want to run before your app really starts up.  One reason my be to create global constances like defautl data base urls.

```js
app.run(function(){});
```

## AngularJs Routing

In your function to get the routes, you will want to return an array of json objects the represent a route object.  The objects contain attributes:

* url
* template
* settings: another hash
* title

Url can contain paramters, they are just : starting words.  ``` /search/:search ```.  You can gain access to these url parameters by adding a dependancy to routeParams.

## AngularJs Services

Services in angualarjs are used to put code that you willneed to use accross all your layers, so that you dont have to have teh logic across all the code.  What kind of things do you see that use the sevices?  The first one that you will probably create is loading data from your server side.  You might access user data across many different controllers, but you dont want to copy the data calls everywhere, so just put it in a service.

The presentor has a service that handles all his logging.  he even attached the logging to create on teh screen toast messages.

How do you create a service??  In angular creating a service is actually called factory and it creates a singleton class across teh whole appliaction.

One of the presentors best practices is to create a common service that is a fecade of all the services that you will commonly add to controllers.  This allows you to not have to have a super long constructor signature.  it all so also you to put small methods you use everywhere on common without having to create a service for a 10 line method.  The example that he uses for this is a isNumber or textContains method.

*Note: presentor created a bootstrap angular nuget package called: hottowel.angular -pre*

Another presentor best practice for creating a service, is to create a service hash object to return. This service object holds the public api for your service.

```js
angular.module('app').factory('nameOfMyService', ['dep1','dep2', myServiceFactoryMethod]);

function myServiceFactoryMethod(dep1, dep2){
	var service = {
		// my services public methods
		save: save,
		getData: getData
	};
	
	return service;
	
	function save(){
		//save code
	}
	
	function getData(){
		//get data code
	}
};
```

## AngularJs Structuring an App

**Be Consistant, Be Consistant**

Make everything easily findable.  Putting everything in one file, does not make it findable.

You can do folders for types, this works well for small projects.  You can do folders for features, this is better for larger projects.  Good example: [Angular Growth Structure](http://www.johnpapa.net/angular-growth-structure/).

Don't put you js code into the script folder, that is for 3rd party code.  When you mix in your code and 3rd party code it makes it harder to find code and to run lint tools.

*Note: A great website for angular is [Year of Moo](http://yearofmoo.com)*

*Note: A great js library for dates in javascript [Moment.js](http://momentjs.com/).*
