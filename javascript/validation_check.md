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



![유효성 검사 결과물](/Users/mac/Desktop/blog/JinHyungBAE.github.io/assets/gif/validationCheckj(simple).gif)                      

​                          간단한 id, password, email 유효성 검사 결과물

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

| 정규식 표현 |                     설명                      |
| :---------: | :-------------------------------------------: |
|    [xy]     |              x,y중 하나를 찾는다              |
|    [^xy]    |       x,y를 제외하고 문자 하나를 찾는다       |
|    [x-z]    |        x~z 사이의 문자중 하나를 찾는다        |
|     \^      |           특수문자를 문자로 인식함            |
|     \b      |        문자와 공색사이의 문자를 찾는다        |
|     \B      |      문자와 공백사이가 아닌 값을 찾는다       |
|     \d      |                 숫자를 찾는다                 |
|     \D      |            숫자가 아닌 값을 찾는다            |
|     \s      |               공백문자를 찾는다               |
|     \S      |           공백이 아닌 문자를 찾는다           |
|     \t      |               Tab 문자를 찾는다               |
|     \v      |          Vertical Tab 문자를 찾는다           |
|     \w      |          알파벳 + 숫자 + _ 를 찾는다          |
|     \W      | 알파벳 + 숫자 + _을 제외한 모든 문자를 찾는다 |

정규식 표현  을 해석해 보면 다음과 같다. 

``` /^[A-Za-z][A-Za-z0-9]*$/.test(str); ```



^ 시작하고 $로 끝난다. 영문대문자 혹은 소문자로 시작한다. 

영문 대문자 혹은 소문자 혹은 숫자 0~9가 온다. 

이것을 test(str)와 비교한다. 그래서 onlyNumberAndEnglish 함수가 영문과 숫자만을 테스트하는 함수가 된 것이다. 

## 2. 시각화 효과

시각화 효과는 크게 두가지로 진행했다, 

1.  input에 text를 입력할 때 유효하지 않게 입력한 경우 x 표시, 유효하게 입력한 경우는 check 표시를 하여 사용자로 하여금 확실히 입력이 잘 되었는지 잘못되었는지 미리 알려주도록 하자. 
2. 나의 결과물을 보듯이 입력한 값이 유효한 상태일 때는 valid로, 유효하지 않은 상태일 때는 invalid로 class명을 주어 css로  invalid 부분을 전체적으로 붉게 하여 사용자로 하여금 다시 제대로 입력하도록 유도하는 시각화 효과를 작업하도록 하자. 

1번을 진행할 때 일정 사이트에서 체크표시와 x표시를 다운받아 사용할 수 있지만 나는 fontawesome에 있는 체크표시와 x표시를 사용했다. 사용하는 방법은 fontawesome.com에 회원가입을 하면 특정 kit값을 알려준다. 중간에 이메일로 확인하는 과정이 있다. Html의 head 안에 src를 아래와 같이 하고 /[자신이 받은 kit값].js로 입력하면 된다. 

```html 
    <script  src="https://kit.fontawesome.com/[kit 값].js"
      crossorigin="anonymous">
    </script>
```

id를 예를 들면 Label 태그 안에 

* span태그로 ID라고 텍스트입력
* input태그로 사용자로부터 id를 입력받는다
* i태그로 체크표시 또는 x 표시를 fontawesome.com에서 받아온다.
* span태그로 나중에 class명에 invalid가 되면 "id 8글자 이상 입력하세요"가 출력된다. 

이것을 html로 정리하면 다음과 같다. 

```html
  <label class="input-form" id="input-id">
          <span>ID</span>
          <input type="text" />
          <i class="fa" aria-hidden="true"></i>
          <span class="message"></span>
  </label>
```

```javascript
function setAsValid(selector) {
  let form = document.querySelector(selector);
  form.classList.remove("invalid");
  form.classList.add("valid");

  let icon = form.querySelector(".fa");
  icon.classList.remove("fa-times");
  icon.classList.add("fa-check-circle");

  let msg = form.querySelector(".message");
  msg.textContent = "";
}
```

위의 setAsValid함수는 label 상위태그로 div의 클래스명이 form인데

유효하게 사용자가 입력한 경우, 그 form 의 selector로 받아 클래스명에 invalid를 삭제하고 valid 클래스명을 추가한다. 

다음에 아이콘은 x 표시(fa-times)를 삭제하고 check 표시를 하기 위해 class명 'fa-times'를 삭제하고, 'fa-check-circle'를 추가한다. 다음에 회원 가입 버튼위에 위치한 message를 담는 div 태그에 빈 문자열을 출력한다. 

css파일을 살펴보면 class명이 invalid가 되면 background와 text color가 붉은 색 계통으로 변하게 설정해두었다. 

```css 
:root {
    --invalid-text-color: rgb(177, 59, 69);
    --invalid-border-color: rgba(177, 59, 69, .2);
    --invalid-background-color: rgba(255, 192, 203, 0.493);
    --valid-text-color: rgb(51, 173, 51);
 }  
.input-form.invalid {background-color: var(--invalid-background-color);
​    color: var(--invalid-text-color);
​    border-bottom: 1px solid var(--invalid-border-color);
}
```

  



