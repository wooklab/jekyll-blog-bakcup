---
layout: post
title: ElasticSearch Alias
categories:
 - ElasticStack
 - BigData
tags:
 - elasticsearch
---

# Indices Alias
Alias는 하나의 indices에 별칭을 주거나 복수개의 indices에 별칭을 주어 사용할 수 있다.<br/>
ElasticSearch에서 문서들의 집합을 나타내는 indices<sup>인덱스</sup>는 고유의 이름을 갖게 된다.
하지만 여러 인덱스를 묶어 사용하거나 서비스의 편의성을 위해 Alias<sup>별칭</sup>를 사용하게 된다.

<!-- more -->

# Indices에 Alias 추가하기
## URI로 추가하기
```bash
PUT /${인덱스명}/_alias/${alias명}
```
`인덱스명`의 경우 콤마(Comma)를 구분자로 하여 여러 인덱스에 alias를 추가 할 수 있으며, wildcard-expression(\*) 표현식을 통해 일치하는 다수의 인덱스에 alias를 추가 할 수 있다.<br/>
(모든 인덱스에 alias를 추가하고자 하는 경우에는 `_all` 을 사용 하면 된다.<br/>
e.g. PUT /\_all/\_alias/service-group)<br/>


## JSON형식으로 추가하기
```bash
POST /_aliases
{
  "actions" : [
    {
      "add" : {
        "index" : "${추가대상 인덱스명}", 
	"alias" : "${추가대상 alias명}"
      }
    }
  ]
}
```
URI 방식보다 JSON으로 내용을 구체적을 작성함에 있어 약간의 귀찮음이 있을 수 있지만, 명시적이며 안전하다.

---

# Indices에 Alias 제거하기
## URI로 제거하기
```bash
DELETE /${인덱스명}/_alias/${alias명}
```
URI 방식의 경우, 작성을 하던 도중에 실수로 엔터키<sup>Enter</sup>라도 치게 되면 잘못된 인덱스의 alias를 삭제할 수 있다. 개인적으로는 JSON으로 내용을 작성하는 것을 추천한다.

## JSON형식으로 제거하기
```bash
POST /_aliases
{
  "actions" : [
    {
      "remove" : {
        "index" : "${제거대상 인덱스명}", 
	"alias" : "${제거대상 alias명}"
      } 
    }
  ]
}
```

---

# Indices에 Alias 변경하기
```bash
POST /_aliases
{
  "actions": [
    {
      "remove": {
        "index": “${제거대상 인덱스명}“,
        "alias": “${제거대상 alias명}“
      }
    },
    {
      "add": {
        "index": “${추가대상 인덱스명}“,
        "alias": “${추가대상 alias명}”
      }
    }
  ]
}
```
JSON내용을 자세히 보면 `"actions"`라는 항목의 값을 배열로 정의하고 있다. 즉 여러 개의 <b>alias추가/alias삭제</b>에 대한 요청을 한꺼번에 날릴 수 있다.<br/>
Elasticsearch를 어떻게 사용하느냐에 따라 다르지만, 먄약 무중단 서비스에 사용되고 있다면 무중단 서비스를 위해 alias를 swtiching 할 경우가 있다. 이런 경우 해당 액션 배열을 활용하면 스위칭이 가능하다.<br/>




