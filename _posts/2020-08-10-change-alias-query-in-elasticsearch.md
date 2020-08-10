---
layout: post
title: Elasticsearch Alias 변경하기
categories:
 - elasticsearch
tags:
 - elasticsearch
---

# Elasticsearch Alias란
> Elasticsearch에서는 서비스의 운용을 유연하게 하기 위해 Index의 별칭을 추가하여 사용할 수 있는 Alias라는 것이 존재한다. 서비스 중인 인덱스가 있고 무중단으로 신규 인덱스로 교체를 하고 싶다면, Alias를 활용하여 가능하다.

<!-- more -->

# Elasticsearch Alias Query

## Alias 추가하기

> PUT /{인덱스명}/_alias/{Alias명}
<br/>

## Alias 삭제하기

> DELETE /{인덱스명}/_alias/{Alias명}
<br/>

## Alias 교체하기

> POST /_aliases
```json
{
  "actions": [
    {
      "remove": {
        "index": “{제거대상 인덱스명}“,
        "alias": “{제거대상 alias}“
      }
    },
    {
      "add": {
        "index": “{추가대상 인덱스명}“,
        "alias": “{추가대상 alias}”
      }
    }
  ]
}
```
`actions`안에 나열된 `Alias add/remove` 동작은 트랜잭션 처리가 되기 때문에 무중단으로 교체가 가능하다.