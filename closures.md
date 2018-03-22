FUNCTION WITHIN A FUNCTION
RETURN THE INNER FUNCTION
SET IT TO A VARIABLE


closures - enclosed scope
function outer(){
    outer function scope
    function inner(){
        inner function scope
    }
}
returns whatever is to the right of the return


has access because of the snapshot

function outer(){
    var num =0;
    function inner(){
        return ++num
    }
    return inner
}

var one = outer();
one()
var two = outer();
two()
one()
snapshot of the lexical environment -- 
invoke outer -- takes a snapshot of all references in scope chain all the way
up to the global scope
Garbage collector -- which parts don't need to be used anymore //so no memory overload

return inner function from an outer -- garbage collector doesn't get rid of it

return inner function -- takes a snapshot of all variables up to the global scope

invoke the outer function -- you get a snapshot

from that point, invoke the inner function, and it'll update
invoke a second time? - starts at 0 again -- each invocation gets own snapshot of lexical environment
--each invocation has own snapshot of lexical environment

if you invoke the first function 'one()' again, it'll look at its own snapshot and run the program of that snapshot

module pattern - create private variables -- 
store it in closure so you can invoke the function multiple times, but keeps it protected from other scope

function closure(){
    var numn = 0;
    return {
        inc: function(val) {
            num+=val
            console.log(num)
        }
        dec: function (val) {
            num -= val;
            console.log(num)
        }
    }
}
var closure1 = closureIam();
closure1.inc(100);


CONTEXT -> constructor function -> classes
THIS is the keyword that should pop into your mind
as long as we set context correctly -- we can use the same code, but depending on context, it can refer to different data

DEFAULT
IMPLICIT
EXPLICIT

DEFAULT VALUE OF THIS?
this always refers to global scope -- the window -- if you don't set context of this, it'll treat it as the window object
bad practice to modify the global scope

IMPLICIT CONTEXT
TO THE LEFT OF THE DOT

let me = {
    saying: 'cool cool cool',
    iSay: function (){
        alert(this.saying)
    }
}
context is set on the invocation of a function

invoking iSay, it'll check if it is explicitly bound to anything, am i implicitley bound to anything -- is there anything to the left of the dot -- 

explicit context
let me = {
    saying: 'cool cool cool',
    
}
iSay: function (){
        alert(this.saying)
    }
iSay.bind(me)
it'll return the function
once you invoke it -it'll invoke the function with the value of me

explicit always comes first
 
 let you = {
     saying :'not cool cool cool'
 }

 let boundIsay = me.iSay.bind(you)
 boundIsay()
 bind returns a bound copy of a function 
 
 me.iSay.call(you) -- sets the context and calls it right away
 me.iSay.apply(you) -- first argument is always the context, anything after is the arguments for the function
 apply passes in all arguments as one array -- pass in each item one by one into the function

 CONSTRUCTORS

 function objCreator(name){
     return {
         name:name
     }
 }
 objCreator('Joe')

 BETTER WAY

 function UserCreator(name, coder){
     this.name = name
     this.isACoder = coder
 }

 capitalized -- create new object

 let newUser = new UserCreator('Joe', true) -- creates a new instance of an
 empty object then fills that object -- safer way of creating new stuff -- 
 won't pull it onto the global scope
 new sets the context of this and returns this

 typeof -- checks the type


 build a prototype function instead of putting the function right on the constructor -- every constructor function has an object attached to it with the functions attached -- prototype object

 Animal.prototype.makesSound = function

 global constructors -- Array, Number, etc.
each one has prototypes built in -- map, pop, push, pop -- have access to methods through prototypes

Arrow functions - what are they? why do we use them?

function Person (){
    this.age = 0;
    setInterval(function(){
        this.age++;
        console.log(this.age)
    })
}
why does it break?
when you use ES5 functions like this--the context of THIS gets lost
arrow functions fix this
they do not set their own value for the context of THIS
what is the enclosing scope?

use fat arrow functions in life cycle methods -- sets the context as the parent, a life cycle method, which means the THIS context will have the react methods


CLASSES - JS, not react

class Animal {
    constructor(){
        this.type = type;
        this.sound = sound;
    }
}
if I wanted to do same thing as a constructor look above