JSON Diff
http://jsondiff.com/

JSON Beautifier
https://jsonbeautifier.org/

JSON Parser
https://jsonparser.org/

JSON Validator
https://tools.learningcontainer.com/json-validator/

``` js
// JSON
// JavaScript Object Notation

// 1. Object to JSON
// stringify(obj)
let json = JSON.stringify(true);
console.log(json);

json = JSON.stringify(['apple', 'banana']);
console.log(json);

const rabbit = {
    name: 'tori',
    color: 'white',
    size: null,
    birthDate: new Date(),    
    jump: () => {
        console.log(`${name} can jump!`);
    }
}

json = JSON.stringify(rabbit);
console.log(json);

json = JSON.stringify(rabbit, ['name', 'color', 'size']);
console.log(json);

json = JSON.stringify(rabbit, (key, value) => {
    console.log(`key: ${key}, value: ${value}`);
    // return key === 'name' ? 'ellie' : value;
    return value;
});
console.log(json);

// 2. JSON to Object
// parse(json)
console.clear();
json = JSON.stringify(rabbit);

const obj = JSON.parse(json);
console.log(obj);

const obj2 = JSON.parse(json, (key, value) => {
    console.log(`key: ${key}, value: ${value}`);
    return key === 'birthDate' ? new Date(value) : value;
});
console.log(obj2);

rabbit.jump();
// obj.jump();

console.log(rabbit.birthDate.getDate());
// console.log(obj.birthDate.getDate());
console.log(obj2.birthDate.getDate());
