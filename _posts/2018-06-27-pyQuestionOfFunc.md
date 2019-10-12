---
layout: post
title:  "파이썬 함수 관련 몇가지 문제 풀이"
date:   2018-06-27 10:00:00 +0900
categories: python
comments: true
---

## 1번 문제
~~~python
x = 3
z = x
print(id(x) == id(z))
~~~
위의 코드를 출력해보면 결과값이 `True`가 나온다.


그렇다면 아래의 코드는 결과값이 어떨까?
~~~python
x = 1
z = x
x += 121212
print(id(x) == id(z))
~~~
출력해보면 `False`라는 결과값이 나온다.
위의 두 코드가 다른 점은 x를 수정했다는 것이다.
수정만 했을 뿐인데 두 결과값은 정반대의 결과가 나왔다.


이번엔 **integer**가 아닌 **list**를 이용하여 확인해보자.
~~~python
x = [1]
z = x
print(id(x) == id(z))
~~~
위의 코드의 출력값은 `True`이다.

~~~python
x = [1]
z = x
x.append(3)
print(id(x) == id(z))
~~~
위의 코드의 출력값 역시 `True`이다.

**integer**가 아닌 **list**를 이용했는데
결과값이 `True`로 나왔다.

**integer**로 만든 것과 **list**로 만든 것의 차이가 무엇이길래 결과가 다른 것일까?

핵심은 **mutable과 immutable**이다.
**mutable**한 **list**같은 경우, 값(value)을 변경해도 mutable하기 때문에 같은 name을 가진다.
하지만 **immutable**한 **integer**의 경우, 값(value)을 변경하면 immutable하기에 x와 z의 name이 다르며 값도 다르다.
즉, 메모리 공간에 새로운 **integer**가 하나 더 생기게 된다.
따라서 Mutable object와 Immutable object를 잘 알고있어야 위와 같은 오류를 범하지 않을 수 있다.

## 2번 문제
~~~python
def foo(k):
    k = [1]
q = [0]
foo(q)
print(q)
~~~

출력값을 `[1]`이라고 착각할 수 있다.
하지만 코드를 작성해보고 실행해보면 출력값이 `[1]`이 아니라 `[0]`이 출력된다.
어떻게 된 일일까?

- line 3 (`q = [0]`) : q라는 메모리 상자에 `[0]`이 들어간다(초기화된다).
- line 4 (`foo(q)`) : foo함수에 의해 `[0]`을 가지고있는 메모리 상자를 가르키는 name이 q인 동시에 k가 된다.
- line 2 (`k = [1]`) : `[1]`을 가지는 메모리 상자를 가르키는 name이 k로 변하게 된다. 즉, 이 순간 기존 q와 동일한걸 가르키던 k는 이제 새로운 `[1]`이라는 공간을 가르키게 된다.
- line 5 (`print(q)`) : q라는 메모리 상자안에 있는 `[0]`이 출력된다.

위와 같은 절차에 의해 출력이 `[0]`으로 출력되는 것이다.

## 3번 문제
~~~python
def foo(x):
    x[0] = ['def']
    x[1] = ['abc']
    return id(x)
q = ['abc', 'def']
print(id(q) == foo(q))
~~~

출력값이 `True`일까 `False`일까?
출력 해보면 `True`가 출력된다.
어떻게 된 일일까?

- line 5 (`q = ['abc', 'def']`) : q라는 메모리 상자에 `['abc', 'def']`가 들어간다(초기화된다).
- line 6 (`print(id(q) == foo(q))`) : id(q)에는 q의 identity가, foo(q)에는 foo함수에 의해 리턴값이 나오게 된다.

list는 mutable하기 때문에 q로 메모리 상자의 값을 변경가능(=mutable)하다. 따라서, 변경 이후에도 여전히 x, q 모두 **변경된**리스트를 가르키게 된다.
이러한 절차로 인해 `print(id(q) == foo(q))`를 하게 되면 `True`라는 값이 나오게 된다.

### 추가질문
`print(q)`를 하게 되면 어떤 출력값을 보여줄까?
`['abc', 'def']`? 아니면 `[['def'], ['abc']]`??


**[['def'], ['abc']]가 출력된다.**
foo함수에서 0번째, 1번째 요소를 변경시켰기 때문이다.

## 4번 문제
~~~python
def foo(i, x = []):
    x.append(x.append(i))
    return x
for i in range(3):
    y = foo(i)
print(y)
~~~

1, 2, 3번 문제와 비교해봤을 때, 좀 더 난이도가 있다.
위의 결과값을 알아내기 위해서는 아래 두 코드에 대한 이해가 필요하다.

### 4-1번 문제
~~~python
l = []
l.append(1)
x = l.append(1)
type(x)
~~~
위의 코드를 실행시켜보면 출력값이 `NoneType`이라 출력된다.
어떻게 된 일일까?

우리는 `l.append(1)`을 주목해야 한다.
`x = l.append(1)`을 실행시키면 l이라는 리스트에 `[1]`이 추가된다.

이 때, `l.append(1)`은 `l`이라는 객체의 함수를 부르는 것이고 그 함수(append)가 `None`을 `return`하기 때문에 사실상 위 라인은 `x = None`과 동치이다.
만약, `l.append(1)`가 인풋으로 받은 인자를`return`하는 함수였으면 `x = 1`일 것이다.
하지만 파이썬의 list라는 타입(클래스)을 만든 사람들이 `.append`라는 함수를 그렇게 설계하지 않았기 때문에 x는 `None`이 되는 것이다.
[(python 공식문서 - append 함수 부분 참고)](https://docs.python.org/3.6/tutorial/datastructures.html)
4번 질문으로 다시 돌아가서 `x.append(x.append(i))`부분을 보자.
위의 설명에 의해 `x.append(i)`부분은 `None`값이라는 것을 알 수 있다. 따라서 `x`리스트에 `None`을 덧붙이게 된다는 것을 알 수 있다.

### 4-2번 문제
~~~python
def foo(x = []):
    x.append(2)
    print(x)
foo()
foo()
foo()
~~~
위의 코드를 이해해야한다.
foo함수를 한번 호출(call)하면 `[2]`, 두번 출력하면 `[2, 2]`, 세번 출력하면 `[2, 2, 2]`가 출력된다.

위의 두 코드에 대한 이해가 되었다면 본론으로 돌아가자.

(4번 문제 내용)
~~~python
def foo(i, x = []):
    x.append(x.append(i))
    return x
for i in range(3):
	y = foo(i)
print(y)
~~~

4번 문제의 코드실행을 살펴보면,
- line 4 (`for i in range(3)`) : i = 0, 1, 2가 순서대로 초기화된다.
- line 5 (`y = foo(i)`) : 함수가 호출되면서 foo함수 내부(`x.append(2)`)가 실행된다.
- line 2 (`x.append(x.append(i))`) : `None`값을 계속 추가시킨다. 또한 첫번째 줄 함수 매개변수에 `x = []`라는 것이 있기 때문에 i = 0일 때, print(y)를 하게 되면 `[0, None]`이 출력된다.

추가적으로, 함수를 부를 때(call)마다 매번 `x = []`가 초기화 되는게 아니라 맨 처음에 파이썬 인터프리터가 이 코드를 한번 쭉 읽기 시작할 때 **단 한번만** 초기화된다.
따라서 마지막 줄(`print(y)`)를 실행하게 되면 `[0, None, 1, None, 2, None]`이 출력되게 된다.

### 참고글

- [Tricky Python I : Memory Management for Mutable & Immutable Objects](https://medium.com/@tyastropheus/tricky-python-i-memory-management-for-mutable-immutable-objects-21507d1e5b95)
- [Mutable vs Immutable in Python](https://medium.com/@meghamohan/mutable-and-immutable-side-of-python-c2145cf72747)
