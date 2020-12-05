---
title: "First met with Go-Lang"
date: 2020-12-04 23:05
categories: Go-Lang Study
---
## Go Language
Go 언어는 컴파일 언어이고, Java 와 같이 GC 기능을 제공.
Go 는 단순하고 간결한 프로그래밍 언어를 지향하고 Communicating Sequential Processes (CSP) 스타일의 Concurrent 프로그래밍을 지원

Python 과 유사하게 소스코드는 해당 소스 코드가 속한 package 를 명시하는 `package name` 키워드로 시작되고 함수의 선언은 `func name() {}` 으로 이루어짐

변수의 사용은 다음과 같음
```go
   var a int // a 라는 정수 변수의 선언
   var f float32 = 11. // float32 타입의 변수 f 에 11.0 이라는 초기값 할당

   // 대입문을 사용해 변수에 저장된 값을 변경할 수 있으며, 초기값이 지정되지 않은 변수의 값은 0으로 초기화됨
   a = 3
   f = 12.0
```

상수의 사용은 다음과 같음
```go
  // 상수는 키워드 const 를 사용해 선언
  const c int = 10
  const s string = "Hi"

  // Go 언어는 할당값을 보고 타입을 추론할 수 있다
  // 위와 아래는 결과적으로 같은 의미
  const c = 10
  const s = "Hi"

  // 여러 상수를 괄호 안에 나열해 사용할 수 있다
  const (
    Visa = "Visa"
    Master = "MasterCard"
    Amex = "American Express"
  )

  // 상수값을 0부터 부여하기 위해 iota 라는 identifier 사용 가능
  const (
    Apple = iota  // 0
    Grape         // 1
    Orange        // 2
  )
```

Go 언어의 데이터 타입
1. 부울린 타입 ; `bool`
2. 문자열 타입 ; `string`
3. 정수형 타입 ; `int int8 int16 int32 int64 / uint uint8 uint16 uint32 uint64`
4. Float 및 복소수 타입 ; `float32 float64 complex64 complex128`
5. 기타 타입
  - `byte` ; uint8 과 동일하며 Byte 코드에 사용
  - `rune` ; int32 와 동일하며 유니코드 코드포인트에 사용

문자열

Reference : [예제로 배우는 Go 프로그래밍][예제로-배우는-Go-프로그래밍]

[예제로-배우는-Go-프로그래밍]: http://golang.site/
