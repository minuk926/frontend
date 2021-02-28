#### 미정의 값 체크 : Nullish coalescing operator - ??
```js
+ null, undefinded, NaN, '', 0  : false
+ {}, [] : true
+ 실행블록 참 : if(!xx)  
+ 실행블록 거짓 : if(!!xx)
+ 미존재 초기화 : xx || 'default'
  + 앞이 거짓인 경우 실행 : xx || 실행문
  + 앞이 참인 경우 실행 : xx && 실행문
```
#### ES6 추가( ~ 2015)
```js
* template string
  ss + ' Lee' === \`${ss} Lee\`
* Symbol : 유니크한 값 생성  
* Symbol('Mark') !== Symbol('Mark')   
* String('Mark') === String('Mark')
* Shorthand property names  
    + const elle3 = {
      name,    // name: neam
      age      // age: age
    };
    const name = 'elle1';
    const age = '20';
    const elli2 = {
      name: name,
      age: age
    };

* Destructing Assigment  
    + const { name, level } = student;
    + const {name: studentName, level: studentLevel} = student;  // studentName과 studentLevel로 할당
        const student = {
          name: 'Anna',
          level: 1
        };
        const name = student.name;
        const level = student.level;
    + const [first, second] = animals;
        const animals = ['tiger','dog'];
        const first = animals[0];
        const second = animals[1];

* Spread sintax : deep copy 아님에 주의 - call by refference
    + const fruits = [...fruits1, ...fruits2];
    + const dog = {...dog1, ...dog2};
        {
          const obj1 = {key: 'key1'};
          const obj2 = {key: 'key2'};
          const array = [obj1, obj2];
        }  
        const arrayCopy = [...array];
        const arrayCopy2 = [...array, {key: 'key3'}];
        const dog1 = {key: 'dog'};
        const dog2 = {key1: 'tiger', key:'cat'};
        con dog3 = {...dog1, ...dog2};    //동일한 key는 override 됨

* Default parameters
    + function printMsg(message = 'default messge'){};

* Ternary Operrator
    + const component = isCat ? 'cat': 'dog';

* Template Literals
    + `Today weather is ${weather} and temparature is ${temparature}.`
```    
#### ES11(2020)  
```js
* Optional chaining
    + console.log(person.job?.manager?.name);
        const person1 = {
          name: 'Ellie',
          job: {
            title: 'S/W Engineer',
            manager: {
              name: 'Bob'
            }
          }
        };
        const person2 = {
          name: 'Bob'
        }

        {
          function printManager(person){
            console.log(persion.job.manager.name);
          }
          printManager(person1);
          printManager(person2);    // error

* Nullish coalescing operator
    + const userName = name ?? 'Guest';
    const name = '';
    const num = 0;
    const userName = name ?? 'Guest';       // name || 'Guest' --> 'Guest'
    const message = num ?? 'undefined';     // num || 'undefined' --> 'undefined'
```    
#### Promise
```js
function p() {
    return new Promise(/* exceutor*/(resolve, reject) => {
        setTimeout(() => {
            //resolve('1000ms 후에 fullfilled!!');
            reject(new Error('1000ms 후에 reject!!'));
        }, 1000)
    });
};
p().then(result => console.log(result))
   .catch(e => console.log(e))
   .finally(() => console.log('end'));
//1. pending : 생성(executor)자 이용 생성
//2. resolve() : 이행(fulfilled),  reject() : 거부(rejected)

// value는 Promise 객체 또는 Object
Promise.resolve(/*value*/).then()... 
Promise.reject(/*value*/).catch()...
Promise.all([Promise Object]).then()...
Promise.race([Promise Object]).then()...
```    
#### async - await
```js
// async가 추가된 메소드는 Promise.resolve() 형태로 return
async function pp(ms) {
    return setTimeout(() => {
        return ms;
    }, ms);
};

// async 함수에서 await로 사용
// reject 처리는 try - catch로 처리
(async function () {
    try {
        const result = await pp(1000);
        console.log(`${result} ms 후 완료`);
    } catch (error) {
        console.error(`에러발생 :: ${error}`);
    } finally {
    }
})();

async function aa(){ 
    try{
      const results = Promise.all([p1(), p2(), p3()]);
      const result = Promise.race([p1(), p2(), p3()]);
    }catch(error){
    } finally {
    }
};    
```    
#### Deep Copy : 배열([]) 도 동일
```js
// 1 Depth
let a = { name:"name1", value:"value1"};  // []
// 1. slice - Deep copy
let aa = a.slice();
// 2. spread operation
let aaa = {...a}
// 3. assign - Deep copy
Object.assign(aaa, a);    // 병합
// 4. forEach - - Deep copy
let obj = {};
Object.keys(a).forEach(function(key){
    obj[key] = obj[key];
});

// 1 Depth over
let a = {
    kk : {
        name: 'kkk';
    };
    ss : 'dhhd"
};
let scp = JSON.parse(JSON.stringify(a));
```   
#### 배열내장 함수
```js
const array = [1, 2, 3, 4, 5, 6, 7, 8];
let newArr = null;
forEach : array.forEach(n => {
            newArr.push(n*n);
          });
map : newArr = array.map(n => n*n);

const superheroes = ['아이언맨', '캡틴 아메리카', '토르', '닥터 스트레인지'];
indexOf : const idx = superheroes.indexOf('토르');   // 2

const todos = [
    {id: 1, text: '자바스크립트 입문', done: true},
    {id: 2, text: '함수 배우기', done: true},
    {id: 3, text: '객체와 배열 배우기', done: true},
    {id: 4, text: '배열 내장함수 배우기', done: false}    
];
findIndex : const idx = todos.findIndex(todo => todo.id === 3);  // 2
find : const todo = dodos.find(todo => todo.id === 3); // {id: 3, text: '객체와 배열 배우기', done: false}
filter : taskNotDone = todos.filter(todo => !todo.done); // [{id: 4, text: '배열 내장함수 배우기', done: false}]
splice / slice : 항목제거 / 배열추출(새로운 배열 생성 - 기존 배열 유지)
    const numbers = [10, 20, 30, 40];
    const sliced = numbers(0,2);    // [10,20]
    const idx = numbers.indexOf(30);
    numbers.splice(idx, 1);  // 30 삭제 - [10,20,40]
shift(맨앞배열제거), unshift(맨앞배열추가) / pop(맨뒤배열제거) 
concat-배열을 합친다(기존배열유지) / join
reduce :  reduce((acc, cur) => acc + cur, 0) - 콜백함수, 함수 초기값
    let sum = numbers.reduce((acc, cur) => acc + cur, 0);
    let sum2 = numbers.reduce((acc,cur) => {
        console.log({ acc, cur });
        return acc + cur;
    }, 0);
```    
