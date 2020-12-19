---
title: "Interview Review - DB"
date: 2020-12-16 21:30
categories: Interview
---

## Interview 내용 중

- Database 란?

여러 사람이 공유해 사용할 목적으로 체계화해 통합, 관리하는 데이터의 집합이다. 논리적으로 연관된 하나 이상의 자료를 모은 것으로, 그 내용을 구조화함으로써 검색, 갱신의 효율화를 꾀한 것이다. 즉, 몇 개의 자료 파일을 조직적으로 통합해 자료 항목의 중복을 없애고 자료를 구조화해 기억시켜 놓은 자료의 집합체라 할 수 있다.

공동 자료로서 각 사용자는, 같은 데이터라 할지라도 각 응용 목적에 따라 다르게 사용이 가능하다.

- 왜 사용하는가?

프로그램을 만들다보면 사용자들에 의해 생성된 데이터, 프로그래머가 필요에 의해 넣은 데이터 등 필연적으로 데이터가 많이 생성된다. 만약 데이터베이스를 사용하지 않는다면, 이 데이터들은 프로그램이 종료되는 순간 모두 날아가게 되고 이러한 현상을 방지하고 데이터들을 저장하기 위해 데이터베이스를 사용한다.

- Database 용어

![Database_terms](/images/database_terms.png)

**식별자 (Identifier)** : 여러 집합체를 담고 있는 관계형 데이터베이스에서 각각의 구분할 수 있는 논리적인 개념

**식별자의 특성**
	- 유일성 : 하나의 Relation 에서 모든 행은 서로 다른 키 값을 가져야 한다.
	- 최소성 : 꼭 필요한 최소의 속성들로만 키를 구성해야 한다.

	?

Reference :

[데이터베이스 Wikipedia][데이터베이스-Wiki]

[코딩팩토리 Database][코딩팩토리-Database]

[데이터베이스-Wiki]: https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4
[코딩팩토리-Database]: https://coding-factory.tistory.com/77#recentEntries
