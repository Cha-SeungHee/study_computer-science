``` js 
// Ternary Operator
// ❌ Bad Code 💩
function getResult(score) {
    let result;
    if (score > 5) {
        result = '👍';
    } else if (score <= 5) { // Unnecessary 'else if'
        result = '👎';
    }

    return result;
}

// ✅ Good Code ✨
function getResult(score) {
    return score > 5 ? '👍' : '👎';
}


// Nullish coalescing operator
// ❌ Bad Code 💩
function printMessage(text) {
    let message = text;
    if (text == null || text == undefined) {
        message = 'Nothing to display';
    }
    console.log(message);    
}

// ✅ Good Code ✨
function printMessage(text) {    
    const message = text ?? 'Nothing to display'; 
    console.log(message);
}

// 🚨 Default parameter is only for undefined (not null)
function printMessage(text = 'Nothing to display') {
    console.log(text);
}

// 🚨 Logical OR operator ||
function printMessage(text) {
    const message = text || 'Nothing to display';
    console.log(message);
}

const result = getInitialState() ?? fetchFromServer();
console.log(result);

function getInitialState() {
    return null;
}

function fetchFromServer() {
    return 'Hiya from 💻';
}


// Object Destructuring
const person = {
    name: 'Julia',
    age: 20,
    phone: '01077777777',
};

// ❌ Bad Code 💩
function displayPerson(person) {
    displayAvatar(person.name);
    displayName(person.name);
    displayProfile(person.name, person.age);
}

// ❌ Bad Code 💩
function displayPerson(person) {
    const name = person.name;
    const age = person.age; // 여전히 person. 반복

    displayAvatar(name);
    displayName(name);
    displayProfile(name, age);
}

// ✅ Good Code ✨
function displayPerson(person) {
    const { name, age } = person;
    displayAvatar(name);
    displayName(name);
    displayProfile(name, age);
}


// Spread Syntax - Object
const item = { type: '👔', size: 'M' };
const detail = { price: 20, made: 'Korea', gender: 'M' };

// ❌ Bad Code 💩
item['price'] = detail.price;

// ❌ Bad Code 💩
const newObject = new Object();
newObject['type'] = item.type;
newObject['size'] = item.size;
newObject['price'] = detail.price;
newObject['made'] = detail.made;
newObject['gender'] = detail.gender;

// ❌ Bad Code 💩
const newObject2 = {
    type: item.type,
    size: item.size,
    price: detail.price,
    made: detail.made,
    gender: detail.gender,
}

// ✅ Good Code ✨
const shirt0 = Object.assign(item, detail);

// ✅ Better! Code ✨
const shirt = { ...item, ...detail };
// Spread syntax의 장점: 기존의 값을 업데이트 할 수 있음
const shirt = { ...item, ...detail, price: 40 };


// Spread Syntax - Array
let fruits = ['🍏', '🍋', '🍑'];

// fruits.push('🍓');
fruits = [...fruits, '🍓'];

// fruits.unshift('🥝');
fruits = ['🥝', ...fruits];

const fruits2 = ['🍌', '🍉', '🍒'];
let combined = fruits.concat(fruits2);
combined = [...fruits, '🍒', ...fruits2];


// Optional Chaining
const bob = {
    name: 'Julia',
    age: 20,
}

const anna = {
    name: 'Julia',
    age: 20,
    job: {
        title: 'Software Engineer',
    },
};

// ❌ Bad Code 💩
function displayJobTitle(person) {
    if (person.job && person.job.title) {
        console.log(person.job.title);
    }
}

// ✅ Good Code ✨
function displayJobTitle(person) {
    if (person.job?.title) {
        console.log(person.job.title);
    }
}

// ✅ Good Code ✨
function displayJobTitle(person) {
    const title = person.job?.title ?? 'No Job Yet';
    console.log(title);
}


// Template Literals (Template String) 
const person = {
    name: 'Julia',
    score: 4,
}

// ❌ Bad Code 💩
console.log(
    'Hello ' + person.name + ', Your current score is: ' + person.score
);

// ✅ Good Code ✨
console.log(`Hello ${person.name}, Your current score is: ${person.score}`);

// ✅ Good Code ✨
const { name, score } = person;
console.log(`Hello ${name}, Your current score is: ${score}`);

// ✅ Good Code ✨
function greetings(person) {
    const { name, score } = person;
    console.log(`Hello ${name}, Your current score is: ${score}`);
}


// Looping
const items = [1, 2, 3, 4, 5, 6];

// ❌ Bad Code 💩
function getAllEvens(items) {
    const result = [];
    for (let i = 0; i < items.length; i++) {
        if (items[i] % 2 === 0) {
            result.push(items[i]);
        }
    }
    return result;
}

// Better
function getAllEvens(items) {
    return items.filter(num => num % 2 === 0);
}

function multiplyByFour(items) {
    const result = [];
    for (let i = 0; i< items.length; i++) {
        result.push(items[i] * 4);
    }
    return result;
}

// Better
function multiplyByFour(items) {
    return items.map(num => num * 4);
}

function sumArray(items) {
    let sum = 0; 
    for (let i = 0; i < items.length; i++) {
        sum += items[i];
    }
    return sum;
}

// Better
function sumArray(items) {
    items.reduce((a, b) => a + b, 0);
}

const evens = getAllEvens(items);
const multiple = multiplyByFour(evens);
const sum = sumArray(multiple);
console.log(sum);

// ✅ Good Code ✨
const evens = items.filter((num) => num % 2 === 0);
const multiple = evens.map((num) => num * 4);
const sum = multiple.reduce((a, b) => a + b, 0);
console.log(sum);

// ✅ Good Code ✨
const result = items
    .filter((num) => num % 2 === 0)
    .map((num) => num * 4)
    .reduce((a, b) => a + b, 0);
console.log(result);
