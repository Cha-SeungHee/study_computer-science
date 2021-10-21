``` js
// async & await
// clear style of using promise : )

// 1. async
async function fetchUser() {
    return 'ellie';
}

const user = fetchUser();
console.log(user);

// 2. await
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

/*
async function getApple() {
    await delay(1000);
    return '🍎';
}

async function getBanana() {
    await delay(1000);
    return '🍌';
}

// callback hell
/*
function pickFruits() {
    return getApple()
    .then(apple => {
        return getBanana()
        .then(banana => `${apple} + ${banana}`);
    })
}
*/

/* 비동기 작업을 동기작업 마냥 작성할 수 있다는 장점 */
/*
async function pickFruits() {
    const apple = await getApple();
    const banana = await getBanana();
    return `${apple}` + `${banana}`;
}
*/

/* 에러 처리의 경우
async function getApple() {
    await delay(1000);
    throw 'error';
    return '🍎';
}

async function getBanana() {
    await delay(1000);
    return '🍌';
}

async function pickFruits() {
    try {
        const apple = await getApple();
        const banana = await getBanana();    
    } catch() {

    }

    return `${apple}` + `${banana}`;
}
*/


async function getApple() {
    await delay(2000);
    return '🍎';
}

async function getBanana() {
    await delay(1000);
    return '🍌';
}

// 사과와 바나나를 따는 일은 서로 독립적
// 위의 경우처럼 각 작업을 순차적으로 기다릴 필요가 없다
// 동시에 수행하면 된다
// 아래의 방법이 가능하나 실제로는 3번처럼 쓴다
async function pickFruits() {
    const applePromise = getApple();
    const bananaPromise = getBanana();
    const apple = await applePromise;
    const banana = await bananaPromise;
    return `${apple} + ${banana}`;
}

pickFruits().then(console.log)

// 3. useful Promise APIs
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log);

function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
}
pickOnlyOne().then(console.log);
