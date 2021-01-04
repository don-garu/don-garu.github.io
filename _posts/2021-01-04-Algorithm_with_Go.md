---
title: "Baekjoon with Golang"
date: 2021-01-04 21:10
categories: Study algorithm golang
---

## Go 언어로 알고리즘 문제 풀이 (코딩 테스트 대비)

Go 언어는 기본적인 내용들에 대해서밖에 공부를 하지 않아서, 알고리즘 코딩에 사용되는 입출력 / 간단한 알고리즘 STL 과 같은 내용 등을 정리하고자 한다.

- 콘솔에서 입력받기

GoLang 에서 콘솔로 입력을 받는 방법은 여러 가지가 있다고 하는데, 그 중 가장 직관적으로 보이는 `newReader` 로 사용을 해 보려고 한다. `bufio` 패키지에 속한 `bufio.NewReader()` 를 호출함으로써 입력을 받을 수 있고 `NewReader` 의 Parameter 에 어떤 소스로부터 입력을 받을 지를 명시할 수 있다.

```go
package main

import {
	"bufio"
}

func main {
	reader := bufio.NewReader(os.Stdin) // os 의 표준 입력으로부터 데이터를 읽어 올 Reader 선언
	str, _ := reader.ReadString('\n') // 어떤 Delimeter 를 기준으로 String 을 읽을 것인지 명시해야 한다
	words := strings.Fields(str) // strings 의 Fields 메소드는 Parameter 를 받아 공백 문자들로 string 을 Tokenizing 한다
}
```

위의 예제와 같은 방식으로 입력을 받을 수 있고, str 을 `strings.Fields()` 메소드를 이용해 tokenizing 한 단어들을 words 로 받아서 처리할 수 있다.

- 두 수 비교하기 [문제 Link][백준-1330]

위의 예제와 같이 string Split / strconv 의 atoi 등을 활용해 문제를 풀었다.

- 최소, 최대 [문제 Link][백준-10818]

위의 문제와 같은 방식으로 문제를 풀었으나 실행 시간이 기존의 C++ 코드 대비 2배 이상, 메모리 사용량은 20배 가량 증가했다. 문제의 원인이 입력 방식에 있는지, 기존 패키지의 메소드를 활용한 점인지 확인하기 위해 각각의 코드를 작성해 보았다.

전체적인 로직은 크게 변하지 않고 입력 자체만 `Reader` 를 사용하던 방식에서 `Scanner` 를 사용하도록 변경한 결과 메모리 사용량은 대략 15% 정도, 수행 시간은 2/3 정도로 감소했다.

추가적으로 `strings` 의 `Atoi` 메소드를 사용하지 않으니 메모리 사용량과 수행 시간이 감소한 걸 확인했다. 정확한 이유는 아직은 모르겠지만.. 일단 알고리즘 문제 풀이에 있어서 `Reader` 를 사용해야 한다는 점은 알게 되었다.


[백준-10818]: https://www.acmicpc.net/problem/10818
[백준-1330]: https://www.acmicpc.net/problem/1330
