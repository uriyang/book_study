# Chapter 01. 데이터 타입
> 코어 자바스크립트: 핵심 개념과 동작 원리로 이해하는 자바스크립트 프로그래밍

## 1. 데이터 타입의 종류
- ```기본형```: 값이 담긴 주솟값을 바로 복제
  - **숫자** (number)
  - **문자열** (string)
  - **불리언** (boolean)
  - **null**
  - **undefined**
  - **심볼** (Symbol) - ES6에서 추가 
- ```참조형```: 값이 담긴 주솟값 묶음을 가리키는 주솟값을 복제
  - **객체** (object)
  - **배열** (Array)
  - **함수** (Function)
  - **날짜** (Date)
  - **정규표현식** (RegExp)
  - **Map, WeakMap** - ES6에서 추가 
  - **Set, WeakSet** - ES6에서 추가 

## 2. 데이터 타입에 관한 배경지식
### 1) 메모리와 데이터
- 1byte = 8bit: 비트를 묶어주므로 검색 시간을 줄인다.
- **메모리 주솟값**: 바이트 단위의 식별자 (위치 파악 가능)
### 2) 식별자와 변수
- **변수**: 변경 가능한 데이터가 담길 수 있는 공간
- **식별자**: 데이터를 식별하는 데 사용하는 이름 (변수명)

## 3. 변수 선언과 데이터 할당
### 1) 변수 선언
- 메모리에서 비어있는 공간을 확보한 후, 공간을 식별자로 지정
### 2) 데이터 할당
- 변수 영역에 데이터 영역의 주솟값을 지정
- 확보된 공간을 변환된 데이터 크기에 맞게 늘리기 어렵기 때문에, 새로운 값 할당 시에는 새로운 데이터 공간의 주소를 연결

## 4. 기본형 데이터와 참조형 데이터
### 1) 불변값
- 변경 가능성의 대상: 변수 영역 메모리
- 불변성 여부의 구분 대상: 데이터 영역 메모리
### 2) 가변값
- 가변 (불변하지 않다)
  - 객체의 변수 영역이 별도로 존재
  - '새로운 객체'가 만들어지지 않고, 기존 객체 내부의 값만 변경
- 참조 카운트가 0이 되면 가비지 컬렉터의 수거 대상이 된다.
### 3) 변수 복사 비교
> 복사 후, 객체 프로퍼티 변경
- 기본형: 참조하는 값이 달라짐
- 참조형: 참조하는 값이 달라지지 않음

## 5. 불변 객체
### 1) 불변 객체를 만드는 간단한 방법
> 얕은 복사만을 수행
```js
var copyObject = function (target) {
  var result = {};
  for (var prop in target) {
    result[prop] = target[prop];
  }
  return result;
};
```
### 2) 얕은 복사와 깊은 복사
- 얕은 복사: 바로 아래 단계의 값만 복사하는 방법
- 깊은 복사: 내부의 모든 값들을 전부 복사하는 방법
```js
var copyObjectDeep = function(target) {
  var result = {};
  if (typeof target === 'object' && target !== null) {
    for (var prop in target) {
      result[prop] = copyObjectDeep(target[prop]);
    }
  } else {
    result = target;
  }
  return result;
};
```

## 6. undefined와 null
- **undefined**를 반환하는 경우
  - 값을 대입하지 않은 변수. 즉 데이터 영역의 메모리 주소를 지정하지 않은 식별자에 접근할 때
  - 객체 내부의 존재하지 않는 프로퍼티에 접근하려고 할 때
  - return 문이 없거나 호출되지 않는 함수의 실행 결과
- **null**
  - 비어있는 값을 명시적으로 나타내고 싶을 때 사용
  - typeof null이 object 임을 주의