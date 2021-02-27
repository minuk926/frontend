# frontend

## CSS 
#### 초기화
```
초기화 참조 : https://www.jsdelivr.com/package/npm/reset-css
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">
```    
#### css Basic Selector
```
> - 자식 : ul > li
+ - 형제 인접 1개 : ul + ol
~ - 형제 : ul ~ ol
space - 자손 : ul li
```    
#### css Pseudo-Elements Selector  
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
#### Attribute Selector
```
[attr], [attr=value] : [class], [disabled], [type=password] or [type="password"]
[attr^=value], [sttr$=value] : [class^="btn-"] or [class^=btn-], [class$=success]
```    
#### Inheritance : 문자를 다루는 속성이 대체로 상속
```
font - font-size, font-weight, font-style, line-height, font-family
color, text-align, text-indent, text-decoration, letter-spacing, opacity
강제 상속 : inherit
```    
#### Style 우선 순위 : !important > 인라인 style > 아이디 > 클래스[:] > 태그[::]
```
1. 명시도 : 점수가 높은 선언 우선 - !important > 인라인 style > 아이디 선택자 > 클래스(:) 선택자 > 태그(::) 선택자 > 전체선택자 > 상속
2. 선언순서 : 점수가 같은 경우 마지막 선언 override
3. 중요도 : 상속 보다 우선 - override
4. !important 적용 최우선
```
#### CSS / 단위
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
#### CSS - 속성
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
### position : static / relative - 자신 / absolute - 부모 / fixed - 뷰포트 / sticky - scroll 영역 
               absolute 권장
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
                transform-origin, transform-style, perspective, perspective-origin, backface-visibility
### animation : animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count
                animation-direction, animation-fill-mode, animation-play-state
### columns : auto, column-width, column-count
              columns: 너비 개수        
              column-gap: 너비;
              column-rule: 두께 종류 색상;
              p {
                columns: 150px 3;
                column-gap: 20px;
                column-rule: 2px solid;
              }
```
#### flex : container / items
```
container : flex가 부여된 요소
            display: flex; - block 요소 처럼 상하로 전개  /   inline-flex; - inline 요소처럼 수평으로 전개
            flex-flow: row nowrap; - 주축 여러줄묶음;   수평[row, row-reverse] / 수직[column, column-reverse]
            flex-wra: nowrap, wrap, wrap-reverse
            justify-content: 주축의 정렬 방법 설정 
                             flex-start, flex-end, center, space-between, space-around
            align-content: 교차축의 정렬 방법 설정 - flex-wrap속성을 통해 items가 여러줄(2줄이상)이고 여백이 있는 경우만 사용 가능
                           stretch, flex-start, flex-end, center, space-between, space-around
            align-items: 교차축의 items 정렬 방법 설정(items가 한 줄일 경우 많이 사용)
                         align-content 속성이 우선 - align-items를 사용하려면 align-content: stretch 로 설정해야 함
                         stretch, flex-start, flex-end, center, baseline(문자열기준 정렬)
items : order / flex(flex-glow, flex-shrink, flex-basis) / align-self
        order: 순서;  - 앞으로, + 뒤로
        flex-grow: 숫자;  item의 증가 너비 비율을 설정, item이 가변 너비가 아니거나 값이 0인 경우는 미 적용됨 
                   item이 3개이고 flex-grow가 1, 2, 1 이면 25 : 50 : 25의 비율의 너비를 가지게 된다
        flex-shrink: 감소너비;  item이 감소하는 너비의 비율 설정  클수록 많이 감소(flex-glow와 동일 형태)   
        flex-basis: 기본너비; item의 공간 배분전 기본 너비 설정 - auto인 경우 width / height로 너비 설정  but 단위값이 부여되면 width/height 설정 불가 
                    flex-basis: 0, flex-glow: 1 --> glow 값 온전히 적용
                    flex-basis: 100px; --> 기본값 유지  여분의 값에 대해 glow 적용
        flex : flex-grow flex-shrink flex-basis;  증가너비  감소너비  기본너비    
               flex: 1, 1, 20px,  flex: 1 1; - 1,1,0  flex: 1 20px; - 1,1, 20px
                     flex-basis 값이 생략되면 auto가 아닌 0이 적용
        align-self : 교차축에서 개별 item의 정렬 방법을 설정,  align-items는 Container 내 모든 items의 정렬 방법을 설정
                     필요에 의해 일부 item만 정렬 방법을 변경 할 경우 align-self 사용 --> align-items 속성보다 우선
                     auto(container의 align-items 속성을 상속 받음) / stretch / flex-start / flex-end / center / baseline
```
#### Grid : Container / items
```
Container : display: grid;  inline-grid;
            grid: grid-template-xxx와 grid-auto-xxx의 단축 속성
                  grid: grid-template
                        grid-template-rows / grid-auto-flow grid-template-columns;
                        grid-auto-flow grid-auto-rows / grid-template-columns;
                        
            grid-template: grid-template-rows / grid-template-columns;
                           grid-template-areas;
            grid-template-rows : 행의 크기 정의                    
            grid-template-columns : 열의 크기 정의 
                                     fr(fraction 비율) -   1fr 1fr -->  1 : 1
                                     repeat - repeat(3, 1fr)
                                     .container{
                                       display: grid;
                                       grid-template-rows: 1행크기 2행크기...;
                                       grid-template-rows: [선이름] 1행크기 [선이름] 2행크기 [선이름] ...;
                                     }
            grid-template-areas : .container{
                                    display: grid;
                                    grid-template-rows: repeat(2, 100px);
                                    grid-template-columns: repeat(3, 1fr);
                                    grid-template-areas:
                                      "header header header"
                                      "main main aside"
                                      ". footer footer";  /* grid를 비우고 싶으면 . 입력 */
                                  }
                                  header{grid-area: header;}
                                  main{grid-area: main;}
                                  aside{grid-area: aside;}
                                  footer{grid-area: footer;}
            row-gap / column-gap / gap : grid 간격   gap: row-gap column-gap;   
            grid-auto-rows / grid-auto-columns : 암시적 행 / 열의 크기 지정
            grid-auto-flow : 배치하지 않은 아이템의 배치 방식 지정
                             row / column / row dense / column dense - dense(빈영역 채움)
            align-content, justify-content: 수직/수평 축 정렬
                           normal(stretch), start, end, center, space-around, space-between, space-evenly(여백고르게), stretch
            align-items, justify-items: 수직/수평 정렬    
                                        normal(stretch), start, end, center, stretch
             
items : grid-row: 1 / 2;    (grid-row-start / grid-row-end)        -->  span 2;
                  grid-row-start: 1;  grid-row-end: 2;  
        grid-column: 1 / 3;  (grid-column-start / grid-column-end) -->  span 3;
                     grid-column-start: 1;  grid-column-end: 3;
        grid-area: 시작 / 시작 / 끝 / 끝;  (grid-row-start / grid-column-start / grid-row-end / grid-column-end)
                   영역이름;
                   grid-area: 2 / span 2 / 3 / -1;     -->  grid-row: 2 / 3;   grid-column: span 2 / -1;
        align-self, justify-self : 각각의 아이템의 수직/수평 정렬
                                   normal(stretch), start, end, center, stretch
        order : 그리드 아이템 배치순서 지정
        z-index : 아이템이 쌓이는 순서 지정
        repeat, minmax, fit-content, fr(fractional unit), min-content, max-content, auto-fill, auto-fit
```
## SCSS - SASS(Syntactically Awesome Style Sheets)의 상위 버전
```
* SCSS / SASS 차이 : {}와 ; 사용 유무(SASS는 사용 안함)
                    믹스인(Mixins) 생성 방법 : 생성 - SCSS : @mixin  사용 - @include
                                                     SASS : =      사용 - + 
* compile : SassMeister(https://www.sassmeister.com/)  
            Parcel - node 환경  
* Syntex
  comment - /* */   
            // : 컴파일시 미 반영
  $ - 변수   
  !global - 전역변수   ( $color: #111 !global; ) 
  & - 중첩 - 상위 선택자 참조   
         @at-root - 중첩안에서 생성하지만 root 범위에서 사용 가능
         : - 중첩된 속성 정의 ( font-, margin-등)
         .section{
             $w: 100px !global;
             $h: 100px;
             &:last-child{
               color: red;
             }
             @at-root .box{
                 width: $w;
                 height: $h;
             }
             font: {
                 weight: bold;
                 size: 10px;
             }    
         }   
  !default - 초기값 설정 : 할당되지 않은 초기값 설정(할당되어 있다면 기존 할당값 사용)  $color-primary: blue !default;  
  #{} - 변수값 대입 : $unquote("Droid+Sans");
                     @import url("http://fonts.googleapis.com/css?family=#{$family}");
                     --> @import url("http://fonts.googleapis.com/css?family=Droid+Sans");
  unquote() - 문자열의 따옴표 제거(SASS 내장 함수)
  @import - sass 파일 임포트 -  url() 함수 사용할 필요 없다 : @import "경로";
            여러 파일을 가져올 경우 : , 로 구분 : @import "header", "footer";
            css로 컴파일 되는 경우 - 확장자 .css /  http:// 로 시작 / url()  /  미디어쿼리가 있는 경우
  Partials(파일분할) : 파일 이름 앞에 _를 붙여 파일을 생성하고 @import로 가져오면 따로 .css로 컴파일 하지 않고 합쳐서 생성.    
                      @import "_header", "_side-menu", "main";   --> main.css로 생성 
                      webpack, Parcel, Gulp 등의 빌드툴에서는 Partials 기능이 필요 없이 설정에 따라 빌드 BUT, 되도록 위의 규칙을 따를 것
  연산 : * - 하나 이상은 반드시 숫자 : 10px * 10
         / - 분모는 반드시 숫자 
             / 연산 사용이 충족 되려면 :  값 또는 그 일부가 변수에 저장되거나 함수에 의해 반환 되는 경우 - width: $x /2;
                                          () 로 묶여 있는 경우 
                                          값이 다른 산술 표현식의 일부로 사용 되는 경우 - font-size: 10px + 12px / 3;
         숫자 : px단위 연산 - %, em, vw 연산시는 반드시 calc() 사용 -  calc(50% - 20px)
         문자 : + 사용
               첫번째 피연산자에 따옴표가 붙어 있다면 결과를 따옴표로 묶는다 - content: "Hello " + World;  --> "Hello World"
                                                                          flex-flow: row + "-reverse" + " " + wrap;  --> row-reverse wrap 
         색상 : color: #123456 + #345678;  --> #468ace  46 - 12+34, 8a -34+56, ce - 56+78 
                background: rgba(50, 100, 150, .5) + rgba(10, 20, 30, .5); --> rgba(60, 120, 180, .5)
                            rgba 연산시는 반드시 알파채널의 값이 같아야만 한다 - 알파값은 연산되지 않는다
                            불투명 opacify(),  투명 transparentize() 합수를 사용하면 영산 가능
                            --> $color: rgba(10,20,30, .5);   color: opacify($color, .3);  --> .5 + .3
                                                              color: transparentize($color, .2) --> .5 - .2
Mixins : 재활용  -  @mixin : 선언,  @include : 사용(포함)  
         & (상위요소 참조) 도 사용 가능 
         인수에 : 을 사용 default 값 지정 가능
         전달할 인수를 명시적으로 지정하여 전달 가능 - size($h: 200px)
         가변인수 : ...  -  @mixin font($style, $weight, $sixe, $family)
                           $font-values: italic, bold, 16px, sans-serif;
                           @include font($font-values...);     font($font-values...)
         @content : 스타일 블록 전달 
                    기존의 @mixin에 선택자나 속성 추가  
                    @mixin icon ($url){
                      &::after{
                        content: $url;
                        @content;
                      }
                    }
                    .box1{
                      @include icon("image/icon1.png");
                    }
                    .box2{
                      @include icon("image/icon2.png"){
                        display: block;
                        position: absolute;
                      };
                    }  
         @extend : 확장 - 다른 선택자의 모든 스타일을 가져와야 하는 경우 사용(java와 동일 개념) -  권장하지 않는다 --> @mixin 사용  
         @function :@function 함수명($매개변수) { @return 값 }  -  사용시 함수명 직접 사용
         if :  if(조건, 참일때, 거짓일때)  -  3항 연산자와 비슷
         @if @else @else if : 조건이 들어가는 () 생력 가능
         @for :  @for $i from 시작 through 종료 - 종료만큼 반복
                 @for $i from 시작 to 종료 - 종료 직전 까지 반복 
         @each : JS의 for in 문과 유사 - List와 Map 반복
                 @each $변수 in 배열데이타,  @each $key, $value in 맵데이타
         @while : @while 조건        
         @mixin size($w: 100px, $h: 100px, $val...){
           width: $w;
           height: $h;
           color: $val
         }
         .box1{
           @include size;
         }
         .box2{
           @include size(100px, 150px);
         }
         .box3{
           @include size(100px, 150px, 1, 2, 3);
         }
* 내장함수 : 색상함수 - mix($color1, $color2), lighten($color, $amount), darken($color, $amount) saturate($color, $amount) desaturate($color, $amount)
                       grayscale($color) invert($color)  rgba($color, $alpha) 
                       opacify($color, $amount) fade-in($color, $amount) transparentize($color, $amount) fade-out($color, $amount)
            문자함수 - unquote($string), quote($string), str-insert($string, $insert, $index),  str-index($string, $substring) 
                      str-slice($string, $start-at, [$end-at]), to-upper-case($string), to-lower-case($string)  
            숫자함수 - percentage($number) round($number) ceil($number) floor($number) abs($number)  min($numbers...) max($numbers...) random()
            List함수 - length($list) nth($list, $n) set-nth($list, $n, $value) join($list1, $list2, [$seperator]) zip($list...) index($list, $value)
            Map함수 - map-get($map, $key) map-merge($map1, $map2) map-keys($map) map-values($map)
            Introspection(관리)함수 - variable-exixts(name)-범위내에 있는지 여부 unit($number)-단위반환 unitless($number) comparable($number1, $number2) - 연산가능여부
```


## JS
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
