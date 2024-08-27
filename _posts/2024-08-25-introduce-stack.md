---
layout: post
title: "[테스트 게시물] 스택!"
author: theo5970
date: 2024-08-25 11:40:00 +0900
category: "Data Structure"
tags: ["c"]
---

> **주의**\
> 이 게시물은 예고없이 삭제될 수 있습니다.
{: .prompt-warning }

## 개요

스택(Stack)이란 가장 마지막에 넣은 원소부터 차례대로 꺼내서 사용하는 자료구조이다.[^lifo]\
스택은 다음 2가지 요소로 구성된다.

| 이름   | 역할                  |
| ---- | ------------------- |
| top  | 스택의 끝 부분 위치         |
| data | 스택의 원소들을 저장하고 있는 배열 |


## 연산

스택의 연산에는 크게 4가지가 있다.

### Push
`push(value)`\
스택의 끝 부분에 `value`을 추가한다.

### Pop
`push(value)`\
스택의 끝 부분에 위치한 값을 반환하고 제거한다.\
만약 스택이 비어있다면 이 연산을 수행할 수 없다.

### Top (또는 Peek)
`top()`\
스택의 끝 부분에 위치한 값을 반환한다.\
만약 스택이 비어있다면 이 연산을 수행할 수 없다.

### Empty
`empty()`\
스택이 비어있는지에 대한 여부를 반환한다.

## 예시

스택 `S`를 하나 만든 다음 아래의 연산을 수행해보자.

```c
push(2) 
push(3) 
push(5)
push(7)
pop()
top()
pop()
pop()
push(1)
pop()
```

각 연산에 따른 스택의 상태는 다음과 같다.

```c
push(2)  // S=[2]
push(3)  // S=[2, 3]
push(5)  // S=[2, 3, 5]
push(7)  // S=[2, 3, 5, 7]
pop()    // Return 7, S=[2, 3, 5]
top()    // Return 5
pop()    // Return 5, S=[2, 3, 5]
pop()    // Return 3, S=[2, 3]
push(1)  // S=[2, 3, 1]
pop()    // Return 1, S=[2, 3]
empty()  // Return False, 왜냐하면 스택에 아직 2개의 원소가 남아있기 때문.
```


## 구현

위 코드는 C 언어 및 구조체를 사용해서 구현했다.

```c
#include <stdio.h>
#include <stdbool.h>
#include <assert.h>

#define STACK_SIZE 64
typedef struct {
    int data[STACK_SIZE];
    int top;
} stack_t;

// 스택 초기화
void stack_init(stack_t *s) {
    s->top = -1;
    for (int i = 0; i < STACK_SIZE; i++) {
	    s->data[i] = 0;
    }
}

// empty: 스택이 비었는지 확인
bool stack_empty(stack_t *s) {
	return s->top == -1;
}

// push: 스택에 원소 추가
void stack_push(stack_t *s, int value) {
	assert(s->top < (STACK_SIZE - 1));
	s->data[++s->top] = value;
}

// pop: 스택의 끝에 위치한 원소를 반환 및 제거한다.
int stack_pop(stack_t *s) {
    assert(!stack_empty());
    return s->data[s->top--];
}

// top: 스택의 끝에 위치한 원소를 반환한다.
int stack_top(stack_t *s) {
	assert(!stack_empty());
	return s->data[s->top];
}
```



[^lifo]: 이와 같은 방식의 자료구조를 LIFO (Last In First Out) 라고 한다.