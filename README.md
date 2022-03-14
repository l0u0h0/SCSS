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
### 변수 사용
```scss
$color: royalblue;
.container {
  h1 {
    color: $color;
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
