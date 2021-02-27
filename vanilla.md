#### 미정의 값 체크 : Nullish coalescing operator - ??
```
+ null, undefinded, NaN, '', 0  : false
+ {}, [] : true
+ 실행블록 참 : if(!xx)  
+ 실행블록 거짓 : if(!!xx)
+ 미존재 초기화 : xx || 'default'
  + 앞이 거짓인 경우 실행 : xx || 실행문
  + 앞이 참인 경우 실행 : xx && 실행문
```
#### ES6 추가( ~ 2015)
```
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
```
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
```
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
```
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
```
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
