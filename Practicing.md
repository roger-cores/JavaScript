
JavaScript(Node JS): My Notes
------




### 1. The tradition: hello world to start


```javascript
console.log("Hello world");
```

    Hello world


### 2. JS Datatypes

Primitive Datatypes

1. Numbers, eg. 123, 120.50 etc.
> **Note:** JS doesnt make a distinction between integer and floating-point values. All numbers in JS are represented as floating-point values. Arithmetic is based on 64-bit IEEE-754 standard.
2. Strings
3. Boolean, true or false.

1. null
2. undefined
> **Note:** Variables can be undefined in the following scenarios:
> 1. Variable isn't declared.
> 2. Variable is declared but isn't initialized.

Non-primitive Datatype:

1. Object


### 3. A lie told often enough becomes the Truth!

The follwoing values are falsy in JavaScript:

1. 0
2. '' (empty string)
3. false
4. null
5. undefined
6. NaN (not-a-number)

All other values are interpreted as truthy by JavaScript



```javascript
var nbs = "non-blank-string";
if(null) console.log("null is truthy"); else console.log("null is falsy");
if(nbs) console.log("non-blank-string is truthy"); else console.log("non-blank-string is falsy")
```

    null is falsy
    non-blank-string is truthy


### 4. Declaring variables


```javascript
var money; //variable declaration
var name = "abc"; //variable initialization
var a,b; //multiple variable declaration
money = 200;
console.log(money+","+name);
```

    200,abc


>**Note:** Use the var keyword only for declaration or initialization, once for the life of any variable name in a document. You should not re-declare same variable twice. Use 'use-strict' expression in ES5 or later to run JavaScript in strict mode.

### 5. Why the *var* keyword is a BIG NO!

When a variable is declared with the *var* keyword anywhere inside a function, it is hoisted as the first line in that function.


```javascript
var globalVar = "globalVar";
var item = "globalItem";
function task(){
    if(globalVar === "globalVar"){
        var item = 5; //this assignment should have affected the code inside the if block
    }
    console.log(item); //expected output is "globalItem" but 5 is printed instead
}

task();
```

    5


The above snippet is equivalent to the following snippet:


```javascript
var globalVar = "globalVar";
var item = "globalItem";
function task(){
    var item = 5;
    if(globalVar === "globalVar"){
        
    }
    console.log(item); //expected output is "globalItem" but 5 is printed instead
}

task();
```

    5


Fix it with the *let* keyword!


```javascript
var globalVar = "globalVar";
var item = "globalItem";
function task(){
    if(globalVar === "globalVar"){
        let item = 5;
    }
    console.log(item); //variable isn't hoisted up
}

task();
```

    globalItem


### 6. Variables like to settle down too!


```javascript
const iAmSelfSatisfied = "enough"; //A constant variable
iAmSelfSatisfied = 1; //cannot do this bro!
```


    evalmachine.<anonymous>:2

    iAmSelfSatisfied = 1; //cannot do this bro!

                     ^

    

    TypeError: Assignment to constant variable.

        at evalmachine.<anonymous>:2:18

        at ContextifyScript.Script.runInThisContext (vm.js:50:33)

        at Object.runInThisContext (vm.js:152:38)

        at run ([eval]:971:15)

        at onRunRequest ([eval]:798:18)

        at onMessage ([eval]:758:13)

        at process.emit (events.js:159:13)

        at emit (internal/child_process.js:790:12)

        at _combinedTickCallback (internal/process/next_tick.js:141:11)

        at process._tickCallback (internal/process/next_tick.js:180:9)


### 7. Checking Equality


```javascript
let itemA = 1, itemB = 2;
console.log(itemA==itemB);
```

    false


The *== (double-equals)* operator automatically converts variables to suitable types


```javascript
itemB = true;
console.log(itemA==itemB); //Since itemB is true and itemA is a truthy value, they both are equal
```

    true


Avoid this ambiguity with the *=== (tripple-equals)* operator


```javascript
console.log(itemA===itemB);
```

    false


### 8. How *== (double-equals)* breaks transitivity!


```javascript
console.log('0'==0); //A equals B | '0' and 0 are both falsy
console.log(0=='');  //B equals C | 0 and blank-string are both falsy
console.log(''=='0');//A does not equal A | blank-string is falsy but '0' (non-blank-string) is a truthy value
```

    true
    true
    false


### 9. Variable Scope

1. Global Variables
2. Local Variables


```javascript
var myVar = "global"; // Declare a global variable
var myVar2 = "global2"; //Declare another global variable
function checkscope( ) {
    var myVar = "local";  // Declare a local variable, even with the same name, local scope is given precedence in this case
    myVar2 = "local2";    // manipulat the value of global variable
    console.log(myVar+","+myVar2);
    
}
console.log(myVar+","+myVar2);
checkscope();
console.log(myVar+","+myVar2);
```

    global,global2
    local,local2
    global,local2


> **Note:** Inside a function in JS, local variable takes precedence over a global variable

### 10. The typeof Operator

<table>
    <tr>
       <th>Type</th>
       <th>Strin returned by typeof</th>
    </tr>
    <tr>
        <td>Number</td>
        <td>"number"</td>
    </tr>
    <tr>
        <td>String</td>
        <td>"string"</td>
    </tr>
    <tr>
        <td>Boolean</td>
        <td>"boolean"</td>
    </tr>
    <tr>
        <td>Object</td>
        <td>"object"</td>
    </tr>
    <tr>
        <td>Function</td>
        <td>"function"</td>
    </tr>
    <tr>
        <td>Undefined</td>
        <td>"undefined"</td>
    </tr>
    <tr>
        <td>Null</td>
        <td>"object"</td>
    </tr>
</table>


```javascript
var a = 10;
var b = "This is a string";
var linebreak;
var d = null;
var e = false;
console.log("Type of a: "+typeof a)
console.log("Type of b: "+typeof b)
console.log("Type of c: "+typeof c)
console.log("Type of d(null): "+typeof d)
console.log("Type of e: "+typeof e)
```

    Type of a: number
    Type of b: string
    Type of c: undefined
    Type of d(null): object
    Type of e: boolean


### 11. Functions


```javascript
function sayHello()
{
    console.log("Called function: Hello world!");
}
console.log("Before calling the function!");
sayHello();
```

    Before calling the function!
    Called function: Hello world!


##### Nested functions


```javascript
function hypotenuse(a,b){
    function square(x) {return x*x;}
    return Math.sqrt(square(a) + square(b));
}

console.log("hypotenuse of a triangle with sides 3 and 4 is "
            + hypotenuse(3,4));
```

    hypotenuse of a triangle with sides 3 and 4 is 5


##### Another way to define a function


```javascript
var func = new Function("x","y","return x*y");

console.log(func(10,20));
```

    200


##### Another way to define a function
Without using the new keyword or defining a function name


```javascript
var func1 = function(x,y){
    return "Full Name: "+x+" "+y;
};
console.log(func1("Ajay","Thorve"));
```

    Full Name: Ajay Thorve


##### The Fat-Arrow functions

The short-hand single-line method of declaring functions. You can define the arguments it takes and the value it returns in one single line.


```javascript
var func1 = (arg1, arg2)=>arg1+arg2;
console.log(func1("Ajay", " Thorve"));
```

    Ajay Thorve


### 12. Functions rule JavaScript

JavaScript supports higher order functions i.e functions that take in functions as their arguments and/or return function as return value.


```javascript
var func1 = function(func2){
    func2();
}

var func2 = function(){
    console.log("this executed inside func2");
}

func1(func2);
```

    this executed inside func2


### 13. Hiding data :)


```javascript
function account(bal){ //cannot be edited because there is no reference to bal outside
    return function(){
        return bal;
    }
}
var accountInstance = account(200);
console.log(accountInstance());
```

    200


### 14. Currying it up a little

Currying refers replacing a function taking arguments with a sequence of functions that give the same result. For example: f(x,y) can be translated to f(g(x))


```javascript
function account(bal, name){ //f(x,y)
    return function(){
        return bal + " " + name;
    }
}

var accountInstance = account(200, "Ajay Thorve");
console.log(accountInstance());
```

    200 Ajay Thorve


The above snippet can be translated to the following snippet:


```javascript
function account(bal){ //f(x)
    return function person(name){ //g(y)
        return bal + " " + name; 
    }
}

var accountBalanceInstance = account(200);
console.log(accountBalanceInstance("Ajay Thorve")); //f(g(y))
```

    200 Ajay Thorve


### 15. Objects


```javascript
var obj = {} //a blank object
```

Objects can take key value pairs. This construct can be nested. Keys should confirm to JavaScript variable name conventions and values can be of primitive, Object or Array type.


```javascript
var bankAccount1 = {
    name: "Roger Correia",
    accountNumber: "E0012",
    balance: "12000"
};
console.log(bankAccount1);
```

    { name: 'Roger Correia',
      accountNumber: 'E0012',
      balance: '12000' }


##### Accessing properties of an object

*followers* is a property inside the object *instagramAccount1*
It can be accessed using period operator as: *instagramAccount1.followers*


```javascript
var instagramAccount1 = {
    name: "Roger Correia",
    handle: "rogeriscorreia",
    accountNumber: "E0012",
    followers: [ //this is an array
        "ajaythorve",
        "maitreyasav",
        "aadmimusafirhai"
    ]
};
console.log(instagramAccount1.followers.length);
```

    3


##### Adding properties

As simple as writing fiction!


```javascript
instagramAccount1.posts = [
    {
        _id: "asldkfjsdf",
        length: 12
    }
]
```




    [ { _id: 'asldkfjsdf', length: 12 } ]



Also why not treat functions equally? They can be added too!


```javascript
instagramAccount1.getPostCount = ()=>instagramAccount1.posts.length; //add a function as property
console.log(instagramAccount1.getPostCount()); //call that function
```

    1


##### Converting primitives to Objects

Primitives can be wrapped inside objects so that more properties can be added to those objects which cannot be done on primitive types.


```javascript
var numberFour = 4;
var objectFour = new Number(numberFour);
numberFour.x = 1;
console.log(numberFour.x); //this was futile
objectFour.x = 1;
console.log(objectFour.x); //this is the cool thing to do!
```

    undefined
    1


Other wrapper methods:


```javascript
var booleanTrue = true;
var objectTrue = new Boolean(booleanTrue);
var objectString = new String("this is a string");
```

##### Creating a closure

We hid data in #13. Let's extend it a bit to create closures. Closures are functions returned by a function. They can be used to hide data while providing some kind of interface that gives limited access.


```javascript
function snapchatAccount(name, handle){ 
    //the variables name and handle are hidden
    //they can be only accessed using functions. They cannot be edited
    return {
        getName: ()=>name,
        getHandle: ()=>handle
    };
}

var scAccount1 = snapchatAccount("Roger", "rogeriscorreia");
console.log(scAccount1.getName());
console.log(scAccount1.getHandle());
```

    Roger
    rogeriscorreia

