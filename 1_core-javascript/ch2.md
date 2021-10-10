# Chapter 02. 실행 컨텍스트
> 코어 자바스크립트: 핵심 개념과 동작 원리로 이해하는 자바스크립트 프로그래밍

## 1. 실행 컨텍스트란?
- 실행할 코드에 제공할 환경 정보들을 모아놓은 객체
- 실행 컨텍스트를 구성하는 방법은 **함수를 실행**하는 것
```js
// ---------------------------- (1)
var a = 1;
function outer() {
  function inner() {
    console.log(a); // undefined
    var a = 3;
  }
  inner(); // ----------------- (2)
  console.log(a); // 1
}
outer(); // ------------------- (3)
console.log(a); // 1
```

## 2. VariableEnvironment
- LexicalEnvironment와 같은 내용을 담지만 최초 실행 시의 스냅샷을 유지
- environmentRecord와 outer-EnvironmentReference로 구성

## 3. LexicalEnvironment
> 처음에는 VariableEnvironment와 같지만 변경 사항이 실시간으로 반영됨.
### 1) environmentRecord와 호이스팅
> 호이스팅: 식별자들을 최상단으로 끌어올린 다음 실제 코드를 실행
#### **[ 호이스팅 규칙 ]**
```js
function hoisting () { // 책에 없는 코드
  var a;
  console.log(a);
  a = 1
  console.log(a);
  console.log(a);
}
hoisting();
```
- 함수 선언은 전체가 끌어올려짐

#### **[ 함수 선언문과 함수 표현식 ]**
- **함수 선언문**: function 정의부만 존재하고 별도의 할당 명령이 없는 것
- **함수 표현식**: 정의한 function을 별도의 변수에 할당
```js
function a() { /* ... */ } // 함수 선언문
var b = functoin () { /* ... */ } // 함수 표현식
```
> 전역 공간에 함수를 선언하거나 동명의 함수를 중복 선언하는 경우가 없어야 한다.

### 2) 스코프, 스코프 체인, outerEnvironmentReference
> 전역공간을 제외하고 **함수**에 의해서만 **스코프 생성**

#### **[ 스코프 체인 ]**
- 스코프 체인 상에서 가장 먼저 발견되 식별자에만 접근 가능
- **변수 은닉화**: 동일한 이름의 변수가 있더라도, 접근이 불가능
#### **[ 전역변수와 지역변수 ]**
- **전역변수**: 전역 스코프에서 선언한 변수
- **지역변수**: 특정 스코프 내에서 선언한 변수

## 4. this
- 실행 컨텍스트의 thisBinding에는 this로 지정된 객체가 저장
