# frontend

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
        }
    })();
    
