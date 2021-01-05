---
title: "Programmers with Golang"
date: 2021-01-04 21:10
categories: Study algorithm golang
---

## Go 언어로 알고리즘 문제 풀이 (코딩 테스트 대비)

어제는 간단한 문제들에 대해 입출력을 어떻게 할 것인지, 알고리즘 해결에 필요한 기본적인 코드 틀은 어떻게 작성하는 지에 대해 공부했다면 오늘은 조금은 더 어려운 로직의 문제들을 풀어보고자 했다.

오늘은 프로그래머스에서 코딩테스트 연습 문제를 가지고 공부를 해 봤는데, 제출 언어에 `GoLang`은 따로 없어서 제출을 하지는 못했다. 그냥 문제를 풀기 위한 로직을 고민하고 Go 언어의 특징을 어떻게 하면 살릴 수 있을까 라는 고민을 해 본 것으로 만족하기로 했다.

- 완주하지 못한 선수 [문제 Link][프로그래머스-42576]

문제 자체는 매우 간단한데, 마라톤에 참여한 선수들의 이름들과 완주한 선수들의 이름들을 입력으로 주고 완주하지 못한 선수의 이름을 찾는 것이다. 원래 C++ 로 문제를 풀었다면 Hash Table 을 생성하고, 각각의 이름에 참여한 수와 완주한 수를 저장하도록 했을 것이다(동명이인이 있기 때문에). 그리고 완주한 사람 수보다 참여한 수가 많다면 완주하지 못한 사람을 찾을 수 있게 될 것이다.

하지만, 우선 GoLang 을 사용하는 이점은 Map 을 사용할 수 있다는 점, 그리고 Go Routine 을 사용해 내부 스레딩이 자유롭다는 점을 생각했다. 일단 Map 을 사용해 Hash Table 을 사용하는 것처럼 사용할 수 있도록 작성하고, C++ 로 작성했을 때는 참여자와 완주자 리스트를 각각 순회하며 숫자를 Counting 해야 했을 것이지만 Go Routine 이라는 좋은 도구가 있기 때문에 이를 활용하기로 했다. 각각의 리스트를 순회하는 동작을 스레드로 따로 분리해서 동작하도록 하고, 메인 스레드는 이를 취합해서 결과만 출력할 수 있도록 했다.

문제 풀이를 위해 작성한 코드는 아래와 같다. 익명함수 두 개를 작성해 각각 테이블에 숫자를 Counting 하도록 하고, 메인 스레드는 두 함수 작업이 완료되면 참여자 명단을 확인해 참여자 수와 완주자 수가 다른 이름을 찾게 된다.

```go
package main

import (
	"fmt"
	"sync"
)

type count struct {
	Pcnt, Ccnt int
}

func main() {
	participant := []string{"marina", "josipa", "nikola", "vinko", "filipa"}
	completion := []string{"josipa", "filipa", "marina", "nikola"}

	fmt.Println(solution(participant, completion))
}

func solution(participant []string, completion []string) string {
	var wait sync.WaitGroup
	wait.Add(2)

	pTable := make(map[string]int)
	cTable := make(map[string]int)

	go func() {
		defer wait.Done()
		for _, name := range participant {
			cnt, exist := pTable[name]
			if !exist {
				pTable[name] = 1
			} else {
				pTable[name] = cnt + 1
			}
		}
	}()

	go func() {
		defer wait.Done()
		for _, name := range completion {
			cnt, exist := cTable[name]
			if !exist {
				cTable[name] = 1
			} else {
				cTable[name] = cnt + 1
			}
		}
	}()

	wait.Wait()

	for _, name := range participant {
		cnt1, _ := pTable[name]
		cnt2, _ := cTable[name]
		if cnt1 != cnt2 {
			return name
		}
	}
	return ""
}
```

- 전화번호 목록 [문제 Link][프로그래머스-42577]

전화번호 목록 문제의 풀이는 마찬가지로 해시였지만, C++ 로 풀었다면 조금 더 복잡했을 것 같다. 우선 문제의 목표는 어떤 전화번호가 다른 전화번호의 접두어인 경우가 생길 수 있는 지를 찾는 것이다. 그래서 풀이 방식 자체는, 전화번호를 길이 순으로 정렬하고, 길이가 짧은 전화번호부터 해시테이블에 저장한다. 이 때, 해싱을 하는 과정에서 생기는 모든 값들에 대해 해시테이블에 존재하는 지 확인하게 되면 접두어가 있는 지 없는 지를 확인할 수 있다.

C++ 로 문제를 풀었을 경우 문자열이 숫자로 구성되어 있어 0~9 값이 가능하고, 총 길이가 20 이하이기 때문에 10개의 값을 표현하는 4 Bit 씩 총 80 Bit 를 필요로 하게 된다. 이렇게 되면 해싱한 값이 Unique 하게 Mapping 이 될 수 없기 때문에 동일한 Hash Key 를 갖는 값에 대해서는 strcmp 를 통해 비교를 한다던지, 혹은 long long 데이터를 두 개를 사용해 두 번만 비교를 한다던지 하는 방식의 구현이 필요하게 된다.

하지만 Go Lang 에서의 Hash Table 은 Map 을 사용할 것이기 때문에 이런 고민은 필요하지 않았다. 그저 전화번호를 길이 순으로 정렬하는 방법에 대해 알고, Map 을 사용할 줄만 알면 결과를 얻을 수 있었다. 물론 제출은 할 수 없기 때문에, 이러한 코드가 수행 속도가 어느 정도 될 지에 대해서는 알 수 없지만... 우선 성능보다는 구현을 할 수 있다는 점에 초점을 맞춰서 공부를 하고 있기에 이 정도로 만족하기로 했다.

```go
package main

import (
	"fmt"
	"sort"
)

type ByLength []string

func (s ByLength) Len() int {
	return len(s)
}

func (s ByLength) Swap(i, j int) {
	s[i], s[j] = s[j], s[i]
}

func (s ByLength) Less(i, j int) bool {
	return len(s[i]) < len(s[j])
}

func main() {
	phone_book := []string{"1235", "12", "567", "123", "12"}

	fmt.Println(solution(phone_book))
}

func solution(phone_book []string) bool{
	sort.Sort(ByLength(phone_book))

	fmt.Println(phone_book)
	table := make(map[string]bool)
	for _, phoneNum := range phone_book {
		val := ""
		for _, c := range phoneNum {
			val = val + string(c)

			_, exist := table[val]
			if exist {
				return false
			}
		}
		table[val] = true
	}
	return true
}
```

위의 코드에서 `ByLength Type` 을 선언하고 Len, Swap, Less 메소드들에 대해 선언한 것은 Sort 함수가 입력 Parameter 에 대해 각 메소드들에 대한 구현이 되어있을 것을 요구하기 때문이다.


[프로그래머스-42576]: https://programmers.co.kr/learn/courses/30/lessons/42576
[프로그래머스-42577]: https://programmers.co.kr/learn/courses/30/lessons/42577
