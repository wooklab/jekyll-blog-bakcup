---
layout: post
title: javax validation and null check (JSR 303)
categories:
 - java
tags:
 - java
---

# javax validation 그리고 null 체크 (JSR 303)
Java에서 클래스의 인스턴스변수<sup>또는 전역변수</sup>가 빈값으로 생성되지 않도록 애노테이션을 이용하여 자동검증하는 방법이 있다. 아래의 라이브러리<sup>mavne&gradle</sup>를 dependency 받아 사용할 수 있다. 물론 null체크만 하는 기능만 있는 것은 아니지만 오늘은 null 체크에 대해서만 간략하게 소개하겠다.<br/>
' <b>null</b> '이라는 것은 `값이 없는 상태 또는 값이 부여되지 않는 상태`라고 정의 할 수 있는데, 막상 생각했을 때 개발하는 사람마다 약간씩 다르게 인식할 수 있는 것 같다. 객체 주소가 할당되지 않은 말그대로 `null` 그리고 값이 비어있는 `empty` 두 가지가 대표적 이다. javax validation에서 해당 내용을 구분한 애노테이션이 존재한다. dependecy를 추가하여 라이브러리를 import하고 아래 표에서 정리가 되어 있듯이 상황에 맞게 사용하자.

# 사용전 dependency 받기
### Maven
```xml
<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-validator -->
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.1.0.Final</version>
</dependency>
```

<!-- more -->

### Gradle
```yaml
// https://mvnrepository.com/artifact/org.hibernate/hibernate-validator
compile group: 'org.hibernate', name: 'hibernate-validator', version: '6.1.0.Final'
```

---

# 사용법

| @NotNull           | @NotEmpty          | @NotBlank                |
| ------------------ | ------------------ | ------------------------ |
| null 허용하지 않음 | null 허용하지 않음 | null 허용하지 않음       |
| "" 허용            | "" 허용하지 않음   | "" 허용하지 않음         |
| " "(space) 허용    | " "(space) 허용    | " "(space) 허용하지 않음 |


cc: [JCP<sub>Java Community Process</sub>](https://www.jcp.org/en/jsr/detail?id=380)

