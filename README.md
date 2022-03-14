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