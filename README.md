# frontend

### CSS 초기화
  + 초기화 참조 : https://www.jsdelivr.com/package/npm/reset-css
  + <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">
### css Selector
  + > - 자식 : ul > li
  + + - 형제 인접 1개 : ul + ol
  + ~ - 형제 : ul ~ ol
  + space - 자손 : ul li
### 미정의 값 체크 
  + null, undefinded, NaN, '', 0  : false
  + {}, [] : true
  + 실행블록 참 : if(!xx)  
  + 실행블록 거짓 : if(!!xx)
  + 미존재 초기화 : xx || 'default'
    + 앞이 거짓인 경우 실행 : xx || 실행문
    + 앞이 참인 경우 실행 : xx && 실행문
### ES6 추가
  + template string
    + ss + ' Lee' === \`${ss} Lee\`
  + Symbol : 유니크한 값 생성  
    + Symbol('Mark') !== Symbol('Mark')   
    + String('Mark') === String('Mark')
### Promise
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
### async - await
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
### Deep Copy : 배열([]) 도 동일
    // 1 Depth
    let a = { name:"name1", value:"value1"};  // []
    // 1. slice
    let aa = a.slice();
    // 2. spread operation
    let aaa = {...a}
    // 3. assign
    Object.assign(aaa, a);    // 병합
    // 4. forEach
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
   
