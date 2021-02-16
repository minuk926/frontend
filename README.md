# frontend

# CSS 
### 초기화
```
초기화 참조 : https://www.jsdelivr.com/package/npm/reset-css
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">
```    
### css Basic Selector
```
> - 자식 : ul > li
+ - 형제 인접 1개 : ul + ol
~ - 형제 : ul ~ ol
space - 자손 : ul li
```    
### css Pseudo-Elements Selector  
```
E:hover - mouse over : a:hover
E:active - mouse click : a:active
E:focus - 대화형콘텐츠만 : input:focus
:first-child, last-child : .fruits li:first-child, li:last-child   :first-child, :last-child
:nth-child(n) - n번째 선택 : .fruits li:nth-child(2)
:nth-child(2n), nth-child(n+3) - 2*n2번째, 3+n 부터~ : .fruits li:nth-child(2n), li:nth-child(n+3)
E:nth-of-type(n) - 동일 E(태그) 형제중 n번째 : .fruits p:nth-of-type(1)
E:not(S) - E태그중 S(selector)만 제외 : .fruits li:not(.red)
E::before, ::after - E요소 앞 또는 뒤에 content 삽입(content 속성 필수) : ul li::before{ content: "prefix"; font-weight: bold; color: red;}
```    
### Attribute Selector
```
[attr], [attr=value] : [class], [disabled], [type=password] or [type="password"]
[attr^=value], [sttr$=value] : [class^="btn-"] or [class^=btn-], [class$=success]
```    
### Inheritance : 문자를 다루는 속성이 대체로 상속
```
font - font-size, font-weight, font-style, line-height, font-family
color, text-align, text-indent, text-decoration, letter-spacing, opacity
강제 상속 : inherit
```    
### Style 우선 순위 : !important > 인라인 style > 아이디 > 클래스[:] > 태그[::]
```
1. 명시도 : 점수가 높은 선언 우선 - !important > 인라인 style > 아이디 선택자 > 클래스(:) 선택자 > 태그(::) 선택자 > 전체선택자 > 상속
2. 선언순서 : 점수가 같은 경우 마지막 선언 override
3. 중요도 : 상속 보다 우선 - override
4. !important 적용 최우선
```
### CSS / 단위
```
* em : font-size 해당 폰트의 대문자 M기준
    .container{
      width: 600px;      /* 60em 과 동일 : 폰트크기가 10px이므로 */
      font-size: 10px;   /* font-size: 2em : 본래 폰트 크기의 2배 */ 
    }  
* rem : root의 r을 의미, 즉 html에 지정된 요소에 영향만을 받음
    html{ font-size: 10px; }
    --> .child{
          font-size: 2em;
          width: 20rem;    /* html의 폰트 크기 * rem =  10 * 20 의 크기 */
        }
* 뷰포트 기준 단위 : % 단위 - vw / vh / vmin / vmax
    + vw / vh : 현재 화면의 가로 / 세로의 비율 적용
    + vmax / vmin : 현재의 가로/세로 크기중 큰/작은 쪽의 크기에대한 비율로 적용  
        .container{
          width: 100vw  / 50vw / 25vw ..., 50vmax
          height: 100vh / 75vh ...,        50vmin
        }
```
### CSS - 속성
```
+ box-sizing : border-box - padding + border 포함 크기 계산
              content-box : width / height 만으로 크기 계산
+ display : block, inline, 
            inline-block(인라인블럭 input...) : width, height, margin, padding 등 block 요소 설정 가능
            none(요소 숨김)
            table, table-cell, flex...              
+ overflow : 자식요소의 넘친 부분의 표시에 따라 visible / hidden / scroll(강제 생성) / auto(필요시 생성)
+ opacity : 투명도 0 ~ 1
+ font : font-style - 기울기  font-weight - 두께  font-size - 크기(default 16px) / line-height - 줄높이(줄간격)  font-family - 서체
         font: italic bold 20px / 1.5 "Arial", sans-serif;   font size와 font family 필수
               20px / 1.5 sans-serif;     bold 20px sans-serif;    italic 20px / 1.5 sans-serif
         + font-style : bold / italic / oblique
         + font-weight : nomal(400) / bold(700) / bolder(부모요소보다 두껍게) / lighter(부모요소보다 얇게) / 100 ~ 900 100단위
                     Thin-100, Extra Light-200, Light-300, Normal-400, Medium-500, Semi Bold-600, Bold-700, Extra Bold-800, Black(Heavy)-900
         + line-height : 숫자로 지정하면 배수 1.4 ~ 1.7이 적당  px로 지정하면 글꼴 크기 변경시 재지정 필요 
         + text-align : left / right / center / justify(양쪽 맞춤)
         + text-decoration(line 설정) : none / underline / overline / line-through(중앙선)
         + text-indent : 첫번째줄의 들여 쓰기  백그라운드이미지 사용시 이미지위에 텍스트를 밀어낼 경우 text-indent: -9999px;로 정의
         + letter-spacing(자간), word-spacing(단어간)
### float : 수평정렬 - display 속성값이 대부분 block 으로 변경됨
+ float을 선언한 그룹을 float을 선언하지 않은 그룹과 같이 사용하는 경우 주의 (clear선언시 문제 발생)
+ left / right                 float: left;
+ clear : both / left / right / both  float 속성 제거  clear: both; 
  --> 아래와 같이 부모요소에서 clearfix를 사용하여 해제 
      <div class="clearfix">
        <div class="child"></div>
        <div class="child"></div>
      </div>
      .clearfix::after{
        content: "";
        clear: both;
        display: block; /* ::after가 인라인요소이므로 block선언 */
      } 
      .child{
        float: left;
      }           
### position : static / relative - 자신 / absolute - 부모 / fixed - 뷰포트 / sticky - scroll 영역 - absolute 사용 권장
               diaplay 가 block으로 변경(absolute/fixed인 경우)
               top / left / right / bottom 함께 사용
    absolute : position(static제외)이 지정된 부모요소 기준으로 배치 - relative 권장)
    sticky : 반드시 top: 0 로 지정(IE 미지원)
    pozition > z-index(position이 있을때만 적용) > html 마지막 코드
### background: background-color  background-image  background-repeat(반복:repeat)  background-position  background-attachment(스크롤:scroll);
                background: red url(...) no-repeat left top scroll;
                background: red url(...) no-repeat right 100px;
                이미지 삽입시 크기 필수
                background-repeat : repeat, repeat-z, repeat-y, no-repeat
                background-position : 방향1, 방향2(top left bottom right center) / x축값, y축값 혼용도 가능 - left 50px
                background-attachment : 배경이미지 스크롤 방식지정
                                        scroll(요소를 따라 스크롤) / fixed / local(요소내 스크롤시 스크롤)
                background-size : auto / cover(비율유지, 넓은쪽 기준, 잘릴수 있다) / contain(비율유지, 짧은쪽 기준, 잘리지 않는다)
                                  auto, contain 또는 width 만 입력 권장
                                  width만 입력시 비율에 맞게 지정됨(width height 순 - width만 지정 권장)
### Transitions : CSS 전환 효과 지정 
                  transition: width 1s, background 1s;
                  transition-property : all 기본 - width, background 처럼 , 로 구분 지정
                  transition-duration : 1s 등
                  transition--timing-function : ease / linear / ease-in / ease-out / ease-in-out / steps(n)
                  transition-delay
### transform : 요소 변형 효과 지정
                transform: 원근 이동 크기 회전 기울임 
                translate(x,y)  translateX(x)  translateY(y)   translate3d(x,y,z) translateZ(z)
                scale(x,y)  scaleX(x)  scaleY(y)   scale3d(x,y,z) scaleZ(z)
                rotate(degree)    rotate3d(x,y,z,a) rotateX(x) rotateY(y) rotateZ(z) 
                skew(x-deg, y-deg)  skewX(x-deg)  skewY(y-deg)  
                perspective(n) - 원근법(거리)
                matrix(n,n,n,n,n,n)
```
# JS
### 미정의 값 체크 : Nullish coalescing operator - ??
```
+ null, undefinded, NaN, '', 0  : false
+ {}, [] : true
+ 실행블록 참 : if(!xx)  
+ 실행블록 거짓 : if(!!xx)
+ 미존재 초기화 : xx || 'default'
  + 앞이 거짓인 경우 실행 : xx || 실행문
  + 앞이 참인 경우 실행 : xx && 실행문
```
### ES6 추가( ~ 2015)
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
### ES11(2020)  
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
### Promise
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
### async - await
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
### Deep Copy : 배열([]) 도 동일
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
