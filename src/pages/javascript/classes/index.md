---
title: Classes
---
## Classes

<!-- The article goes here, in GitHub-flavored Markdown. Feel free to add YouTube videos, images, and CodePen/JSBin embeds  -->
JavaScript does not have the concept of classes inherently. 

But we could simulate the functionalities of a class by taking advantage of the prototypal nature of JavaScript.

This article assumes that you have a basic understanding of <a href="/javascript/prototypes/">prototypes</a>.

For the sake of clarity let us assume that we want to create a class which can do the following

```javascript
var p = new Person('James','Anderson'); // create a new instance of Person class
	p.log() // Output: 'I am James Bond' // Accessing a function in the class
	// Using setters and getters 
	p.profession = 'spy'
	p.profession // output: James bond is a spy
```

### Using Class keyword

Like any other programming language you can now use the `class` keyword to create a class.

This is not supported in older browsers and was introduced in ECMAScript 2015.

```javascript
class Person {
    constructor(firstName, lastName) {
        this._firstName = firstName;
        this._lastName = lastName;
    }

    log() {
        console.log('I am', this._firstName, this._lastName);
    }

    // setters
    set profession(val) {
        this._profession = val;
    }
    // getters
    get profession() {
        console.log(this._firstName, this._lastName, 'is a', this._profession);
    }

}

```
<br />
<br />

`class` is just a syntactic sugar over javaScript's existing prototype-based inheritance model.

In general programmers use the following ways to create a class in JavaScript

### Using methods added to prototypes:

Here all the methods are added to prototype

```javascript
function Person(firstName, lastName) {
    this._firstName = firstName;
    this._lastName = lastName;
}

Person.prototype.log = function() {
    console.log('I am', this._firstName, this._lastName);
}

// This line adds getters and setters for the profession object. Note that in general you could just write your own get and set functions like the 'log' method above.
// Since in this example we are trying the mimic the class above, we try to use the getters and setters property provided by JavaScript
Object.defineProperty(Person.prototype, 'profession', {
    set: function(val) {
        this._profession = val;
    },
    get: function() {
        console.log(this._firstName, this._lastName, 'is a', this._profession);
    }
})

```

You could also write prototype methods over function `Person` as below

```javascript
Person.prototype = {
    log: function() {
        console.log('I am ', this._firstName, this._lastName);
    }
    set profession(val) {
        this._profession = val;
    }

    get profession() {
        console.log(this._firstName, this._lastName, 'is a', this._profession);
    }

}

```

### Using methods added internally

Here the methods are added internally instead of prototype

```javascript
function Person(firstName, lastName) {
    this._firstName = firstName;
    this._lastName = lastName;

    this.log = function() {
        console.log('I am ', this._firstName, this._lastName);
    }

    Object.defineProperty(this, 'profession', {
        set: function(val) {
            this._profession = val;
        },
        get: function() {
            console.log(this._firstName, this._lastName, 'is a', this._profession);
        }
    })
}

```


#### More Information:
<!-- Please add any articles you think might be helpful to read before writing the article -->



