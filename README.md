# frontend

### 미정의 값 체크 
  + !!null, !!undefinded, !!NaN, !!'', !!0  : false
  + 참 : if(!xx)  or 거짓 : if(!!xx)
  + xx || 'default'
### ES6 추가
  + template string
    + ss + ' Lee' === \`${ss} Lee\`
  + Symbol : 유니크한 값 생성  
    + Symbol('Mark') !== Symbol('Mark')   
    + String('Mark') === String('Mark')
