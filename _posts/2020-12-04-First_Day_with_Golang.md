---
title: "First met with Go-Lang"
date: 2020-12-04 23:05
categories: Go-Lang Study
---
Go 언어는 컴파일 언어이고, Java 와 같이 GC 기능을 제공.
Go 는 단순하고 간결한 프로그래밍 언어를 지향하고 Communicating Sequential Processes (CSP) 스타일의 Concurrent 프로그래밍을 지원

Python 과 유사하게 소스코드는 해당 소스 코드가 속한 package 를 명시하는 `package name` 키워드로 시작되고 함수의 선언은 `func name() {}` 으로 이루어짐

변수의 사용은 다음과 같이 사용됨
```go
   var a int // a 라는 정수 변수의 선언
   var f float32 = 11. // float32 타입의 변수 f 에 11.0 이라는 초기값 할당

   // 대입문을 사용해 변수에 저장된 값을 변경할 수 있으며, 초기값이 지정되지 않은 변수의 값은 0으로 초기화됨
   a = 3
   f = 12.0
```
