# SCSS
### 중첩
- css에서는 반복적인 container 라는 상위 선택자 사용이 있었겠지만  
중첩 기능을 사용하여 한번만 사용할 수 있음
```scss
.container {
  h1 {
    color: red;
  }
  ul {
    li {
      font-size: 40px;
      .name {
        color: royalblue;
      }
      .age {
        color: orange;
      }
    }
  }
}
```
### 주석
- 두 가지의 주석 처리 방법을 제공
- 기존 css에서의 /**/와 js 등에서 사용하는 // 방법
- css 파일로 컴파일 되었을 때 // 방법으로 주석처리한 코드는 css로 변환되지 않음
- 변환된 후에도 주석이 남아있어야 한다면 기존의 /**/ 방법으로 주석처리해야할 것.
```scss
$color: red;
/* $color: blue; */
// $color: yellow;
```
### 자식선택자
- container의 자식 선택자라는 것을 명확히 하고 싶으면 자식 선택자 앞에 (ul) 꺽쇠를 붙여 (>) 사용
```scss
.container {
  > ul {
    li {
      font-size: 40px;
      .name: {
        color: blue;
      }
      .age: {
        color: red;
      }
    }
  }
}
```
### 상위선택자 참조
- &기호는 `.btn`을 의미
```scss
.btn {
  position: absolute;
  &.active {
    color: red;
  }
}
.list {
  li {
    &:last-child {
      margin-right: 0;
    }
  }
}
.fs {
  &-small { font-size: 12px; }
  &-medium { font-size: 14px; }
  &-large { font-size: 16px; }
}
```
### 중첩된 속성
- 공통된 속성(네임스페이스 부분)을 선택자처럼 중첩되게 지정해줄 수 있다.  
이때 선택자처럼 사용하되 뒤에 `:` 을 붙여주고  
문장이 끝날 때는 `;`을 붙여줘야한다.
```scss
.box {
  font: {
    weight: bold;
    size: 10px;
    family: sans-serif;
  };
  margin: {
    top: 10px;
    left: 20px;
  };
  padding: {
    top: 10px;
    bottom: 40px;
    left: 20px;
    right: 30px;
  };
}
```
### 변수 사용
- `$` 달러 기호를 사용해 띄어쓰기 없이 뒤에 콜론 기호를 붙여 사용
- 유효범위 - 변수가 선언된 공간 안에서만 사용 가능
- 재할당이 가능,  
`.container`의 `top` 속성에는 200px이 붙지만 `.item` 내에서는 100px로 사용  
다만 `.item`의 바깥으로 나가게 된다면 다시 200px로 부여됨
```scss
$color: royalblue;
$size: 200px;
.container {
  position: fixed;
  top: $size;
  h1 {
    color: $color;
  }
  .item {
    $size: 100px;
    width: $size;
    height: $size;
    transform: translateX($size);
  }
}
```
### 연산
```scss
div {
  width: 20px + 20px;
  height: 40px - 10px;
  font-size: 10px * 2;
  margin: 30px / 2;
  padding: 20px % 7;
}
```
```css
div {
  width: 40px;
  height: 30px;
  font-size: 20px;
  margin: 30px/2;
  padding: 6px;
}
```
- `margin`에서 나뉜 결과로 나오지 않은 이유
```scss
span {
  font-size: 10px;
  line-height: 10px;
  font-family: serif;
  font: 10px / 10px serif;
}
```
- 이렇게 `font`라는 단축 속성을 이용할 때 / 기호를 사용하기에  
나누기를 사용할 때는 `margin: (size/2)`로 사용하거냐  
변수에 담아서 사용해야한다.
- 산술 연산자에서는 단위가 기본적으로 같아야한다.
- `calc()` 를 사용하면 단위가 다르더라도 연산이 된다.
### 재활용
```scss
.containe {
  width: 200px;
  height: 200px;
  background-color: orange;
  display: flex;
  justify-content: center;
  align-items: center;
  .item {
    width: 100px;
    height: 100px;
    background-color: royalblue;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
```
- 이 코드를 `@mixin`을 사용해 `@include`로 가져와서 사용 가능
```scss
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  @include center;
  .item {
    @include center;
  }
}
.box {
  @include center;
}
```
- 함수로 인수를 받아 사용하듯 매개변수를 설정해 인수를 받아 사용할 수 있다.
```scss
@mixin box($size) {
  width: $size;
  height: $size;
  background-color: tomato;
}
.container {
  @include box(200px);
  .item {
    @include box(100px);
  }
}
.box {
  @include box(100px);
}
@mixin box($size: 80px, $color: tomato) {
  width: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box(200px, red);
  .item {
    @include box(80px, green);
  }
}
.box {
  @include box;
}
```
- 이와 같이 기본 값을 지정해 사용할 수 있다.  
인수를 여러 개 두어 사용할 수도 있으며 이때 매개변수는 순서대로 지정해줘야한다.
- 혹은 `(80px, green)`대신 `($color: green)`과 같이  
키워드 인수를 지정해줄 수 있다.
### 반복문
- js에서의 반복문
```js
for (let i = 0; i < 10; i += 1 ) {
  console.log(`loop-${i}`)
}
```
`${i}`를 이용해 문자를 보간해 지정해줌
- scss에서의 반복문
```scss
@for $i from 1 through 10 {
  .box:nth-child{#{$i}} {
    width: 100px * $i;
  }
}
```
`#{i}`를 이용해 문자를 보간해 지정해줌
### 함수
- js와 마찬가지로 `function` 키워드를 사용해 함수 사용
- `mixin`은 속성의 모임 정도로 이해하기.
- 함수와 유사한 개념은 `function`으로 사용
```scss
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
@function ratio($size, $ratio) {
  @return $size * $ratio
}
.box {
  $width: 160px;
  width: $width;
  height: ratio($width, 9/16);
  @include center;
}
```
- `css`로 변환되면
```css
.box {
  width: 160px;
  height: 90px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```
- #### 색상내장함수
```html
<div class="box"></div>
<div class="box built-in"></div>
```
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: mix($color, red);
  }
}
```
- `mix()` 함수를 사용해 `royalblue`와 `red` 색상이 섞인 색을 만들 수 있음
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: lighten($color, 10%);
  }
}
```
- `lighten()` 함수를 사용하면 10%만큼 더 밝게 만들어 줄 수 있다.
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: lighten($color, 10%);
  }
  &:hover {
    background-color: darken($color, 10%);
  }
}
```
- `darken()` 함수를 사용하면 10%만큼 더 어둡게 만들어 줄 수 있다.
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: saturate($color, 40%);
  }
}
```
- `saturate()` 함수를 사용하면 채도를 높여줄 수 있다.
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: desaturate($color, 40%);
  }
}
```
- `desaturate()` 함수를 사용하면 반대로 채도를 낮춰줄 수 있다.
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: grayscale($color);
  }
}
```
- `grayscale()` 함수는 두 번째 인수가 필요하지 않으며 회색으로 만들어준다.
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: invert($color);
  }
}
```
- `invert()` 함수는 색상을 반전시키는 효과를 준다.
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &.built-in {
    background-color: rgba($color, .5);
  }
}
```
- `rgba()` 함수는 두 번째 인수로 해당 색상의 투명도를 설정할 수 있다.
- 원래의 `css`에서 사용하는 `rgba`함수는 인수를 네 개로 받아 사용하지만  
`scss`에서 사용하는 `rgba`함수는 두 개의 인수만을 받아 사용한다.
### 가져오기
```scss
@import "./sub.scss";
```
- `@import`를 사용해 다른 파일을 가져올 수 있다.  
`url()` 함수를 사용하지 않아도 되고  
scss 파일이면 확장자명을 적지 않아도 된다.
- `@import "./sub", "./sub2";`와 같이 쉼표를 이용해 두 파일을  
불러올 수도 있다.
### 데이터 유형
```scss
$number: 1;     // .5, 100px, 1em
$string: bold;  // relative, "../images/a.png"
$color: red;    // blue, #FFFF00, rgba(0,0,0,.i)
$boolean: true; // false
$null: null;
$list: orange, royalblue, yellow;
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);
```
- `number` 숫자 뿐 아니고 단위가 붙은 숫자도 취급
- `string` 글자체나 관계, 앞뒤로 따옴표가 붙은 문자열을 취급
- `color` 색상을 의미하는 문자열은 색상 데이터로 취급
- `boolean` 참 거짓을 나누는 데이터
- `null` 널 값을 의미  
널 값을 주면 해당 속성을 없애줄 수 있다.
- `list` 자바스크립트의 배열과 유사한 형태
- `map` 자바스크립트의 객체 데이터와 유사한 형태, 키 밸류의 형태를 지님  
scss에서는 소괄호로 사용