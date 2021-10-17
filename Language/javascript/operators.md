``` js

// 1. String Concatenation
console.log('my' + ' cat') ;
console.log('2' + 1);
console.log(`string literals: 2 + 1 = ${2 + 1}`);


// 2. Numeric Operations
console.log(1 + 1);
console.log(1 - 1);
console.log(1 * 1);
console.log(1 / 1);
console.log(5 % 2);
console.log(2 ** 3);


// 3. Increment, decrement operators
let counter = 2;
const preIncrement = ++counter;
console.log(`preIncrement: ${preIncrement}, counter: ${counter}`);

const postIncrement = counter++;
console.log(`postIncrement: ${postIncrement}, counter: ${counter}`);


// 4. Assignment operators
let x = 3;
let y = 4;
x += y;
x -= y;
x *= y;
x /= y;


// 5. Comparison operators
console.log(10 < 6);
console.log(10 <= 6);
console.log(10 > 6);
console.log(10 >= 6);


// 6. Logical operators: ||, &&, !
// heavy한 operation일수록 뒤에 배치
const value1 = false;
const value2 = 4 < 2;

console.log(` or : ${value1 || value2 || check()}`);

// often used to compress long if-statmenet
// nullableObject && nullableObject.Something

function check() {
    for (let i = 0; i < 10; i++) {
        // waste of time
        console.log("wow");
    }
    return true;
}


// 7. Equality
const stringFive = '5';
const numFive = 5;

// == loose equality, with type conversion
console.log(stringFive == numFive);
console.log(stringFive != numFive);

// === strict equality, no type conversion
console.log(stringFive === numFive);
console.log(stringFive !== numFive);

// object equality by reference
const sh1 = { name : 'sh' };
const sh2 = { name : 'sh' };
const sh3 = sh1;
console.log(sh1 == sh2); // false
console.log(sh1 === sh2); // false
console.log(sh1 === sh3); // true

// equality 
console.log(0 == false); // true
connsole.log(0 === false); // false
console.log('' == false); // true
console.log('' === false); // false
console.log(null == undefined); // true
console.log(null === undefined); // false
