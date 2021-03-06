---
layout: v2_fluid/docs_base
category: getting-started
id: migration
title: Ionic 2 | Getting Started | Migration
header_title: Getting Started - Migration
header_sub_title: Ionic 2 Developer Preview
---

# Migrating from Angular 1

<a class="improve-docs" href='https://github.com/driftyco/ionic-site/edit/ionic2/docs/v2/getting-started/migration/index.md'>Improve this doc</a>


While Angular 2 requires apps to be update for the syntax change, developers can be proactive and make sure their app is upgradable by following best practices and working with [John Papa's Angular Style guide](https://github.com/johnpapa/angular-styleguide) or [Todd Motto's Angular Style guide](https://github.com/toddmotto/angularjs-styleguide). Both of these will provide you with steps you can take to prepare your code for migration.

### ControllerAs Syntax

ControllerAs Syntax is a feature in Angular 1x where instead of binding data to `$scope`, you can bind to the direct instance of the controller instead. This makes migrating a Angular 1x controller to an Angular 2 class much easier. It's fairly easy to migrate to `controllerAs` from a traditional controller:

_index.html_

```html
    <ion-pane ng-controller="MainCtrl">
      <ion-item>
        {{data.text}}
      </ion-item>
    </ion-pane>
```

_app.js_

```javascript
    .controller('MainCtrl', function($scope){
      $scope.data ={
        text: 'Hello World'
      }
    })
```

To convert this to `controllerAs` syntax, you only have to change a few things.

_index.html_

```html
    <ion-pane ng-controller="MainCtrl as main">
      <ion-item>
        {{data.text}}
      </ion-item>
    </ion-pane>
```

_app.js_

```javascript
    .controller('MainCtrl', function(){
      this.data ={
        text: 'Hello World'
      }
    })

```

### TypeScript

TypeScript is a superset of JavaScript that provides ES6 Classes and type annotations in your code. By adopting TypeScript now, you can write your code as ES6 Classes that will be easy to move to Ionic 2\. The best part is that any valid JavaScript is also valid TypeScript, so you can convert your code piece by piece. If we take our controller from before, we can easily convert it to a TypeScript class like this.

_app.js_

```javascript
    .controller('MainCtrl', function(){
      this.data ={
        text: 'Hello World'
      }
    })

```

_app.ts_

```javascript

    export class MainCtrl{
      constructor(){
        this.data ={
          text: 'Hello World'
        }
      }
    }

```

### Project Structure

With Angular 1, it was a practice to keep all your JavaScript together and separate from your templates. Since Ionic 2 and Angular 2 will be moving to a component base setup, you can reorganize your project to help mentally enforce that concept. So a project who's directory could look like this:

```
    |-www/
    |
    |--js/
    |--|-app.js
    |--|-HomeCtrl.js
    |--|-DetailCtrl.js
    |
    |--templates/
    |--|-Home.html
    |--|-Detail.html
    |
    |-index.html

```

Could start to be reorganized to look like this:

```
    |-www/
    |
    |--Home/
    |--|-HomeCtrl.js
    |--|-Home.html
    |
    |--Detail/
    |--|-DetailCtrl.js
    |--|-Detail.html
    |
    |-index.html
    |-app.js
```

Organizing your project like this can help get you in the mindset that each of your app's views/states are a component, with a template and a controller.
