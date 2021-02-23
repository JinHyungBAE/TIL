---
title: "validation check(유효성 검사)"
category:
  - blog

tag:
  - jekyll
  - TIL
  - javascript
date: "2021-02-22 10:00"
author_profile: true
sidebar_main: true
use_math: true
header:

# 목차
toc: true  
toc_sticky: true 
---

## validation check(유효성 검사)



* 유효성 검사(Validation Check) :보통 홈페이지에 회원가입할 때 기본적으로 유효성 검사를 하게 됩니다. 유효성 검사란 사이트가 원하는 조건에 반드시 그 형식을 맞추어서 입력한 것을 검사하는 것을 말합니다. 예를 들어 id를 입력할 때는 8자 이상, 한글 입력은 안되고 오직 영문자(소문자, 대문자)와 숫자만을 사용해야 한다른 것이 있습니다. 비밀번호와 비밀번호 확인락니 동일해야 한다. 



![validationCheckj(simple)](/Users/mac/Downloads/validationCheckj(simple).gif)

​                                   간단한 id, password, email 유효성 검사 결과물

회원가입 버튼을 누를 때 유효성 검사를 모두 하는 것이 아닌

id와 password, confirm password, email를 사용자가 입력할 때 조건이 안맞을 때는 시각화 효과를 css로 구현한다. 

모든 조건에 맞은 경우에는 회원가입에 성공했습니다 라는 alert창을 띄운다. 

만약 조건중 하나라도 맞지 않으면 "필요한 정보를 조건에 맞게 다 입력하지 않았습니다"라는 문구가 회원가입 버튼 위에 보여진다. 

1. 정규 표현식: 
2. 시각화 효과
   1. 유효한 상태를 입력한 경우 체크표시, 아닌 경우는 x 표시: font awesome 사용
   2. invalid(유효하지 않은 상태) 일 때 배경이 붉게 css
3. 이벤트 연결: 클릭이벤트, 키보드이벤트(onkeyup)
4. DOM

## 1. 정규표현식(regular expression: regex)

id를 체크할 때 한글은 안되고 영어 또는 숫자만 가능하다고 유효성 검사를 할 때 다음과 같은 함수를 사용할 수 있다. 

```js
function onlyNumberAndEnglish(str) {
  return /^[A-Za-z][A-Za-z0-9]*$/.test(str);
}
```

Return 다음에 나오는 것이 바로 정교식 표현이다. 출처는 다음과 같다. https://droptable.tistory.com/65



| 정규식 표현 |                    설명                    |
| :---------: | :----------------------------------------: |
|     ^x      |           문자열이 x로 시작한다            |
|     x$      |            문자열이 x로 끝난다             |
|     .x      |         임의의 한 문자를 표현한다          |
|     x+      |            x가 1번이상 반복한다            |
|     x?      |       x가 존재하거나 존재하지 않는다       |
|     x*      |            x가 0번이상 반복한다            |
|    x\|y     |              x또는 y를 찾는다              |
|     (x)     |    ()안의 내용을 캡쳐하며, 그룹화 한다     |
|   (x)(y)    |                     -                      |
|  (x)(?:y)   |                     -                      |
|    x{n}     |        x를 n번 반복한 문자를 찾는다        |
|    x{n,}    |     x를 n번 이상 반복한 문자를 찾는다      |
|   x{n,m}    | x를 n번 이상 m번 이하 반복한 문자를 찾는다 |

|                         정규식 표현                          |                             설명                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| [xy]<br/>[^xy]<br/>[x-z]<br/>\^<br/>\b<br/>\B<br/>\d<br/>\D<br/>\s<br/>\S<br/>\t<br/>\v<br/>\w<br/>\W | x,y중 하나를 찾는다<br/>x,y를 제외하고 문자 하나를 찾는다<br/>x~z 사이의 문자중 하나를 찾는다<br/>특수문자를 문자로 인식함<br/>문자와 공색사이의 문자를 찾는다<br/>문자와 공백사이가 아닌 값을 찾는다<br/>숫자를 찾는다<br/>숫자가 아닌 값을 찾는다<br/>공백문자를 찾는다<br/>공백이 아닌 문자를 찾는다<br/>Tab 문자를 찾는다<br/>Vertical Tab 문자를 찾는다<br/>알파벳 + 숫자 + _ 를 찾는다<br/>알파벳 + 숫자 + _을 제외한 모든 문자를 찾는다 |

정규식 표현  을 해석해 보면 다음과 같다. 

``` /^[A-Za-z][A-Za-z0-9]*$/.test(str); ```



^ 시작하고 $로 끝난다. 영문대문자 혹은 소문자로 시작한다. 

영문 대문자 혹은 소문자 혹은 숫자 0~9가 온다. 

이것을 test(str)와 비교한다. 그래서 onlyNumberAndEnglish 함수가 영문과 숫자만을 테스트하는 함수가 된 것이다. 


