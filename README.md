# Understanding Javascript Closures

## Overview

The following lesson plan consists of 9 activities that introduce students to javascript closures,  includes concepts on execution context, lexical environment, scoping, considerations for function performance and the usage of let, var and const. 
 
`Summary | Understand javascript closures in 9   
 activites: 3 instructor demonstrations, 3 student activities, and 3 review activities.`

### Notes

* In today's class you will cover javascript closures. 

* This lesson assumes student's knowledge with creating regular or factory functions (declarations and expressions), basic understanding of for loops, as well as a basic understanding of assigning values with let, var and const. 


* Stoking curiosity alerts are signals to the instructional staff to engage with students' thoughts and questions. 


* Students should be given a substantial amount of time to work on the activities. Student should feel comfortable with _the unknown_. Reveal bits of the code for students, but the desired outcome is that students feel comfortable independently developing their own code. 

### Learning Objectives

By the end of class, students will be able to:

* Define lexical environment

* Understand and name the difference between local and global scopes.

* Demonstrate how to effectively use function closures. 

* Construct closures and apply them to loops.

* Classify the appropriate time to utilize closures. 


### Time Tracker

| Number        | Activity      | Time  |
| ------------- |:-------------:| -----:|
| 1             | Intro: Instructor Do                                |    0:05|
| 2             | Everyone Do: <br>Curiosity Stoke                    |   0:10 |
| 3             | Instructor Do: <br>  Closure Scope Chain            |   0:10 |
| 4             | Instructor Do:  <br> Call Stack Execution & The Console     |   0:05 |
| 5             | Instructor Do:  <br> Closures in Loops              |   0:05 |
| 6             | Students Do:  <br> Creating & Working With Closures |   0:15 |
| 7             | Students Do: <br>  Closures & Invocation             |   0:15 |
| 8             | Students Do: <br>  Closures & Loops               |   0:15 |
| 9             | Everyone Do: <br> Review Creating Closures         |   0:10 |   
| 10            | Everyone Do: <br> Review Closures in Loops       |   0:10 |
| 11            | Everyone Do: <br> Review Call Stack Execution & IIFE       |   0:10 |
| 12            | Instructor Do:  <br> Considerations for Function Performance              |   0:10 |

- - -

## Class Instruction

### 1. Instructor Do: Welcome & Intro Today's Class (5 min)

* Welcome students to class.

* Introduce today's objective to deep dive into closures, a technique in computer programming, which the class is applying its use in javascript.


### 2. Everyone Do: Stoke Curiosity | Functions & Scoping (10 mins)

#### TAs Do:
* Slack out in #resources channel: [Mozilla's Documentation](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures#:~:text=In%20other%20words%2C%20a%20closure,created%2C%20at%20function%20creation%20time.)

* Apply the definition to the following code.

 #### Share & asses the following code:

```js
var career = "teacher"
// what is the scope of the variable career?
function experience() {
    var years = 5
    // what is the scope of the variable years?
    var resumeString = "I've worked as a " + career + ' for ' + years + " years."
    return resumeString;
}

console.log(experience());
// what is the expected outcome of invoking the experience function?

```

* Give the class up to 2 minutes to assess the code above and share their thoughts on the lexical scoping and what they expect the invocation of the experience function to return 

* If you have a talkative class, popcorn-style call on a student who seems to have an idea, but may have not spoken as much in class. If your class is not as talkative, call on a student who has engaged more in class to break the silence.

* Give a walkthough of the above code to emphasize understanding _lexical scoping_: the variable "career" is a global variable. The global variable makes "career" accessible from anywhere in the code, including within the experience() function. 

* The variable "years" is a local variable that is only accessible within the experience() function. Accessing the years variable outside the experience() function will throw an error.

* Empasize that javaScript uses the scope to manage the variable accessibility.

* Lexical scoping allows nested or "inner" functions to access the variables declared in its outer scope. 




### 3. Instructor Do: Closure Scope Chain (5 mins)
* Go over the __closure scope chain__ of the following code:
  1.   Local Scope (the scope of the closure)
  2.   Outer Functions Scope
  3.   Global Scope

```js
var career = "teacher"
// what is the scope of the variable career?
function experience() {
    var years = 5
    // what is the scope of the variable years?
    function schooling(){
        var timeInSchool = "I've been in school for "
       console.log(timeInSchool + years + " years")
    }
    schooling()
}

experience()
// what is the expected outcome of invoking the experience function?

```

* The experience() function creates a local variable named years and a function named schooling().

The schooling() is the inner function, closure, that is available only within the body of the experience() function.

The schooling() function can access the variables of the outer function, experience() such as the years variable of the experience() function.

Inside the experience() function, we call the schooling() function to display the message of how long the user has been in school for, which will display "I've been in school for 5 years" .


* This introduction should be a warm up to basic console logging and scoping inside of functions. Students should be comfortable with invoking function calls. 

* Call on individual students to "guess" the output of the console.log in the demonstration in your brower's console before executing the code. 

* Note the use of the console.log inside of the experience() function, with the invocation of the function as opposed to the first example which console.logged the function to retrieve the output of the return.


  * **Instructions**

    * Take a few minutes to quickly look through the attached file. With a partner, discuss what you expect to happen when the code is run.

    * Prepare to share your thoughts with the class.

* The function scope is created for a function call, not for the function itself
Every function call creates a new scope ------------------

### 4. Instructor Do: Call Stack Execution & The Console (5 mins)
```js
function experience(title) {
  return function(years){
    var resumeString = "I've worked as a " + title + ' for ' + years + " years."
    return resumeString;
  }
}
let career = experience('professor');
let schooling = experience('grad student');

console.log(career('3')); // "I've worked as a professor for 3 years."
console.log(schooling('8')); // "I've worked as a grad student for 8 years."
```
#### TAs Do:
* Slack out the code from the following Code Pen: [Call Stack Closures](https://bit.ly/34Fmpet) 

#### Walkthrough Code

* **Instructions**
* Read through the code line by line 
* Call on students to help you live-code the activity.
* Share the expected console outputs and explain why the code has an output at the particular execution. Use the comments in the code to guide the discussion.


### 5. Instructor Do: Closures in Loops (5 mins) (High)

* Share the following code:
```js
for (var i = 1; i <= 3; i++) {
  //this for loop executes the code 3 times
    setTimeout(function () {
      // the value of index is captured at the last execution of valuation of index in the for loop
        console.log('after ' + i + ' second(s):' + i);
    }, index * 1000);
}

// what is the expected output of the console log inside of the callback in the setTimeOut method?

```
  * **Instructions**

    * Assess the above code with students line by line. 

    * Before running the above code in the console, ask students what the expected output will be of `i` in the setTimeout() method.

    * If needed, review and research the basic usage of the setTimeout() method for an understanding of how the code will be executed. 

#### Students Do: 
  * Slackout resource on the setTimeOut() method found in the resources link below. 

#### Instructor Do: 
  * Explain that the callback function passed to the setTimeout() is a closure. It remembers the value of index from the last iteration of the loop, which is 4.
  
  * Reiterate that all three closures created by the for-loop share the same global scope to access the value of the index.

  * Make note of how this code would be refactored using the `let` keyword, and principles of `IIFE` which will be reviewed toward the end of the class. 

### 6. Students Do: Creating & Working With Closures (15 mins)
#### TAs DO: 
* Slack out the code and the instructions below.

  * **Instructions**
   
    * From scratch, create a function `greeting()`, that accepts one argument, name, as a parameter and console logs a string with the name.
    * Create an instance of the `greeting()` funtion that outputs a new name, "Jerome"
    * Create a new instance of the `greeting()` function that outputs a new name, "Sara"

    * Identify the local scope and global scope of the lexical environment
  * **Code**
    * Slack out solution:[Closures Activity 1](https://bit.ly/2HP6Fx1)


### 7. Students Do: Closures & Invocation (15 mins)

* **Instructions**
    * With a partner, create a function from scratch `multiplyByTwo()` that receives a single argument and returns the result of the number multiplied by 2
    * Use this CodePen to view an approach to solving this actvity [Closures Activity 2](https://bit.ly/3kGIKhs)  
 
### 8. Students Do: Closures & Loops (15 mins)

  * **Instructions**
      ```js
        function timeCounter() {
          for (let i = 0; i <= 5; i++) {
            /* This for loop will iterate as long as i is less than or equal
        to 5. Use closure that preserves a reference to i at the time of execution.*/

            setTimeout(function() {
              console.log(i)
          }, i * 1000)
          }
        }
        timeCounter();

    ```
    * Assess the code above and what can be found at [Closures Activity 3](https://bit.ly/3eatXZZ)
    
    * Each call to the console.log occurs after the loop has finished, such that the value of i has changed before the console.log executes. 

    * To fix the issue of the instance of the index holding the same value, refactor this for loop to properly that creates a new closure scope in each iteration of the loop.

    * The desired output should look like the following: 

    ```js 
      /* console.log(i) should output
      0 second after call - log 0
      1 seconds after call - log 1
      2 seconds after call - log 2
      3 seconds after call - log 3
      4 seconds after call - log 4
      5 seconds after call - log 5 */
    ```

    * If you need help, use the code from the previous example as a guide.

    * Once you think your code is functioning properly, share it with the person sitting next to you.  

### 9. Everyone Do: Review Creating Closures (Optional)  (10 mins)

* Review [Closures Activity 2](https://bit.ly/2HP6Fx1)

* Slack the solution out to students.


### 10. Everyone Do: Review Closures in Loops (Optional) (10 mins)

* Using an immediately invoked function expression ( or `IIFE`) creates a new scope by declaring a function and immediately executing it.

* Review the refactored code that now passes and instance of index to the function expression.
```js
function timeOutCounter() {
  for (var i = 0; i <= 5; i++) {
    /* Wrapping the child function expression with an instance of `i` passed to the function reevaluatees the scope of the function after execution in the loop.*/
(function(i){
    setTimeout(function() {
    	console.log(i)
	}, i * 1000);
})(i)

  }
}
  
timeOutCounter();

```

### 11. Everyone Do: Review Call Stack Execution & IIFE, Cont. (10 mins)

* Continue to assess the for loop, make sure to answer student questions as they come on how the for loop is being executed. 

```js
function timeCounter() {
  for (let i = 0; i <= 5; i++) {
    /* This for loop will iterate as long as i is less than or equal
to 5. Use closure that preserves a reference to i at the time of execution.*/

    setTimeout(function() {
    	console.log(i)
	}, i * 1000)
  }
}
timeCounter();

```

* Explain a new use of declaring the variable using ES6 and the `let` keyword to declare a variable that is block-scoped.

* The `let` keyword in the for loop creates a new lexical scope in each iteration, which will give you a new index variable in each iteration.

* The new lexical scope of the for loop follows the chain from the previous scope so that the previous value of the index is copied to the new one.

### 12. Instructor Do: Callbacks Performance Considerations  (10 mins) (Critical)

* Assess the code below and walk students through the solution. Comments in the code will help guide your conversation on the activity. 

* Emphasize to students that it's unnecessary to create functions within other functions if closures are not needed for a particular task. 

* Returning functions from functions affects script performance via processing speed and memory consumption.

* Review the previous activities and refactor the code to compare the utility of using closures 

## Additional Resources 
* [Javascript Closures Moz Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
* [Usage of the setTimeOut() Method](https://www.w3schools.com/jsref/met_win_settimeout.asp)
* [For Loop Usage](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)