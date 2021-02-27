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
