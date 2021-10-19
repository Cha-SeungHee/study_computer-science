``` js
// Objects
// one of the JavaScript's data types
// a collection of related data and/or functionality
// Nearly all objects in JavaScript are instances of Object
// object = { key : value };

// 1. Literals and properties
const obj1 = {}; // 'object literal' syntax
const obj2 = new Object(); // 'object constructor' syntax

function print(person) {
    console.log(person.name);
    console.log(person.age);
}

const sh = { name: 'SH', age: 4 };
print(sh);

// with JavaScript magic (dynamically typed language)
// can add properties later
sh.hasJob = true;
console.log(sh.hasJob);

// can delete properties later
delete sh.hasJob;
console.log(sh.hasJob);


// 2. Computed propertie
// key should be always string
console.log(sh.name);
console.log(sh['name']);
sh['hasJob'] = true;
console.log(sh.hasJob);
delete sh['hasJob'];
console.log(sh.hasJob);

function printValue(obj, key) {
    console.log(obj[key]);
}
printValue(sh, 'name');
printValue(sh, 'age');


// e. Property value shorthand
const person1 = { name: 'bob', age:2 };
const person2 = { name: 'steve', age:3 };
const person3 = { name: 'dave', age:4 };
const person4 = makePerson('sh', 30);

function makePerson(name, age) {
    return {
        name: name,
        age: age,
    };
}

// key와 변수의 값이 동일한 경우 생략 가능
function makePerson(name, age) {
    return {
        name,
        age,
    };
}


// 4. Constructor Function
const person5 = new Person('mk', 30);

// 클래스가 없었을 때는 함수를 유사하게 사용
function Person(name, age) {
    // this = {};
    this.name = name;
    this.age = age;
    // return this;
}


// 5. in operator: property existence check (key in obj)
console.log('name' in sh);
console.log('age' in sh);
console.log('random' in sh);
console.log(sh.random);


// 6. for..in vs for..of
// for (key in obj)
console.clear();
for (key in sh) {
    console.log(key);
}

// for (value of iterable)
const array = [1, 2, 4, 5];
for (value of array) {
    console.log(value);
}


// 7. Fun cloning
// Ojbect.assign(dest, [obj1, obj2, obj3....])
const user = { name: 'ellie', age: '20' };
const user2 = user;
console.log(user);

// old way
const user3 = {};
for (key in user) {
    user3[key] = user[key];
}
console.clear();
console.log(user3);

const user4 = Object.assign({}, user);
console.log(user4);

// another example
const fruit1 = { color: 'red' };
const fruit2 = { color: 'blue', size: 'big' };
const mixed = Object.assign({}, fruit1, fruit2);
console.log(mixed.color);
console.log(mixed.size);
