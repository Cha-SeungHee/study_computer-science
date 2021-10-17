``` js
// 1. Use Strict
// added in ES 5
// Use this for Vanilla Javascript
'use strict';



// 2. Variable
// let (added in ES6)
let globalName = 'global name';
{
    let name = 'sh';
    console.log(name)
    name = 'hello'
    console.log(name);
    console.log(globalName);
}
console.log(globalName)

// var (don't ever use this!!)
// var hoisting (move declaration from bottom to top)
// has no block scope



// 3. Constants
// favor immutable data type always for a few reasosn:
// - security
// - thread safety
// - reduce human mistakes
const daysInWeek = 7;
const maxNumber = 5;



// 4. Variable types
// primitive, single item: number, string, boolean, null, undefinned, symbol
// object, box container
// funcntion, first-class function
const count = 17;
const size = 17.1;
console.log(`value: ${count}, type: ${typeof count}`);
console.log(`value: ${size}, type: ${typeof size}`);

// number - special numeric values: infinity, -infinity, NaN
const infinity = 1 / 0;
const negativeInfinity = -1 / 0;
const nAn = 'not a number' / 2;
console.log(infinity);
console.log(negativeInfinity);
console.log(nAn);

// string
const char = 'c';
const brendan = 'brendan';
const greeting = 'hello ' + brendan;
console.log(`value : ${greeting}, type: ${typeof greeting}`);
const helloBob = `hi $ ${brendan}!`; // template literals (string)
console.log(`value : ${helloBob}, type: ${typeof helloBob}`);

// boolean
// false: 0, null, undefined, NaN, ''
// true: any other value
const canRead = true;
const test = 3 < 1;
console.log(`value : ${canRead}, type: ${typeof canRead}`);
console.log(`value : ${test}, type: ${typeof test}`);

// null
let nothing = null;
console.log(`value : ${nothing}, type: ${typeof nothing}`);

// undefined
let x;
console.log(`value : ${x}, type: ${typeof x}`);

// symbol, create unique identifiers for objects
const symbol1 = Symbol('id')
const symbol2 = Symbol('id')
console.log(symbol1 === symbol2);
const gSymbol1 = Symbol.for('id')
const gSymbol2 = Symbol.for('id')
console.log(gSymbol1 === gSymbol2); // true
console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`);



//5. Dynamic typing: dynamically typed language
// Unexpected type change leads to error -> advent of typescript
let text = 'hello';
console.log(text.charAt(0));
console.log(`value: ${text}, type: ${typeof text}`);
text = 1;
console.log(`value: ${text}, type: ${typeof text}`);
text = '7' + 5;
console.log(`value: ${text}, type: ${typeof text}`);
text = '8' / 2;
console.log(`value: ${text}, type: ${typeof text}`);
console.log(text.charAt(0));



// object, real-life object, data structure
const sh = { name: 'sh', age: 20 };
sh.age = 21;
