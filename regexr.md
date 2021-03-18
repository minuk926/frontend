연습용 사이트: [regexr.com/5mhou](https://regexr.com/5ml92)  
테스트 사이트: [regexon.com](https://regexone.com)

### Groups and ranges

| Chracter | 뜻                                     |
| -------- | -------------------------------------- |
| `\|`     | 또는                                   |
| `()`     | 그룹                                   |
| `[]`     | 문자셋, 괄호안의 어떤 문자든           |
| `[^]`    | 부정 문자셋, 괄호안의 어떤 문가 아닐때 |
| `(?:)`   | 찾지만 기억하지는 않음                 |
| `(?=)`   | 전방탐색 '=' 다음에 일치할 텍스트 위치  |
| `(?<=)`   | 후방탐색 '<=' 다음에 일치할 텍스트 위치  |

그룹 - /gr(a|e)y|(and)/gm  
그룹화X - /gr(?:a|e)y|(and)/gm  
/gr[a|e|f-z]y/gm
/^(?=.*[A-Za-z])$/
```js
http://www.forta.com
https://mail.forta.com
ftp://ftp.forta.com
.+(?=:) ==> http:
            https:
            ftp:
.+(:) ==>   http
            https
            ftp 

ABC01: $23.45
HGG42: $5.31
CFMX1: $899.00
XTC99: $69.96
Total items found: 4
(?<=\$)[0-9.]+ ==> 23.45
                   5.31
                   899.00
                   69.96

<HEAD>
<TITLE>Ben Forta`s Homepage</TITLE>
</HEAD>
(?<=\<[tT][iI][tT][lL][eE]\>).*(?=\<\/[tT][iI][tT][lL][eE]\>)  ==> Ben Forta`s Homepage

(?<=\<[tT][iI][tT][lL][eE]\>)는 후방탐색 작업으로 <TITLE>과 일치하며 소비하지 않습니다..   
(?=\<\/[tT][iI][tT][lL][eE]\>)도 같은 방식으로 </Title>과 일치하며, 소비하지 않습니다. 따라서 제목 텍스트만 반환합니다  
```
### Quantifiers

| Chracter    | 뜻                                  |
| ----------- | ----------------------------------- |
| `?`         | 없거나 있거나 (zero or one)         |
| `*`         | 없거나 있거나 많거나 (zero or more) |
| `+`         | 하나 또는 많이 (one or more)        |
| `{n}`       | n번 반복                            |
| `{min,}`    | 최소                                |
| `{min,max}` | 최소, 그리고 최대                   |

/gra?y/gm : gry gray  
/gra*y/gm : gry gray graaay  
/gra+y/gm : gray graaay  
/gra{2}y/gm : graay  
/gra{2,}y/gm : graay graaaay  
/gra{3,4}y/gm : graaay graaaay  

### Boundary-type

| Chracter | 뜻               |
| -------- | ---------------- |
| `\b`     | 단어 경계        |
| `\B`     | 단어 경계가 아님 |
| `^`      | 문장의 시작      |
| `$`      | 문장의 끝        |

/\bYa/gm : Ya~로 시작
/Ya\b/gm : ~Ya로 종료
/\BYa/gm : Ya로 시작되지 않는 Ya

### Character classes

| Chracter | 뜻                           |
| -------- | ---------------------------- |
| `\`      | 특수 문자가 아닌 문자        |
| `.`      | 어떤 글자 (줄바꿈 문자 제외) |
| `\d`     | digit 숫자                   |
| `\D`     | digit 숫자 아님              |
| `\w`     | word 문자                    |
| `\W`     | word 문자 아님               |
| `\s`     | space 공백                   |
| `\S`     | space 공백 아님              |
| `\t`     | tab                         |
| `\v`     | vertical tab                |

### Flag
| Flag     | 의미                         |
| -------- | ---------------------------- |
| g        | global                       |
| i        | Ignore case                  |
| m        | Multi line - 다중라인 검색    |

```js
비밀번호 : /^.*(?=^.{8,15}$)(?=.*\d)(?=.*[a-zA-Z])(?=.*[!@#$%^&+=]).*$/ : 특수문자 / 문자 / 숫자 포함 형태의 8~15자리 이내의 암호 정규식
          /^[A-Za-z0-9]{6,12}$/ : 숫자와 문자 포함 형태의 6~12자리 이내의 암호 정규식
이메일 : /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/i;
핸드폰 : /^\d{3}-\d{3,4}-\d{4}$/
전화번호 : /^\d{2,3}-\d{3,4}-\d{4}$/;

if(!정규식.test(문자열)) alert('오류')
```

youtube 동영상 ID 획득 : ```(?:https?:\/\/)?(?:www\.)?youtu.be\/([a-zA-Z0-9-]{11}```
##### 실제 js 에서 사용
```js
const regex = /(?:https?:\/\/)?(?:www\.)?youtu.be\/([a-zA-Z0-9-]{11}/;
const url = 'http://www.youtu.be/-ZClicWm0zM';
const rslt = url.match(regex);   // 0: 변수값  1: 결과값
```

```  
Hi there, Nice to meet you. And Hello there and hi.
I love grey(gray) color not a gry, graay and graaay. grdy
Ya ya YaYaYa Ya

abcdefghijklmnopqrstuvwxyz
ABSCEFGHIJKLMNOPQRSTUVWZYZ
1234567890

.[]{}()\^$|?*+

010-898-0893
010 898 0893
010.898.893
010-405-3412
02-878-8888

dream.coder.ellie@gmail.com
hello@daum.net
hello@daum.co.kr

http://www.youtu.be/-ZClicWm0zM
https://www.youtu.be/-ZClicWm0zM
https://youtu.be/-ZClicWm0zM
youtu.be/-ZClicWm0zM
```
