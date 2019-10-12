---
layout: post
title:  "UnicodeDecodeError 해결하기 : 파이썬으로 한글 자막 파일 읽기"
date:   2018-07-11 10:00:00 +0900
categories: python
commends: true
---

인터넷에서 한글 자막 파일(cheeze.smi)을 하나 구했다.
일단, 한번 파이썬의 open 함수로 읽어보자.

~~~python
with open("cheeze.smi", "r") as f:
    print(f.readline())
~~~

하지만, 다음과 같은 에러가 발생한다.

~~~
Traceback (most recent call last):
  File "cheeze.py", line 5, in <module>
    print(f.readlines())
  File "/usr/local/Cellar/python/3.6.5_1/Frameworks/Python.framework/Versions/3.6/lib/python3.6/codecs.py", line 321, in decode
    (result, consumed) = self._buffer_decode(data, self.errors, final)
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe9 in position 2018: invalid continuation byte
~~~

open이라는 함수가 codecs.py 를 불렀고 그 codecs.py에서 `utf-8` 코덱으로 cheeze.smi를 읽으려 시도했으나 실패했다. (`UnicodeDecodeError: 'utf-8' codec can't decode byte`)
파이썬은 `encoding` argument를 따로 주지 않으면 디폴트로 `utf-8`을 이용해 디코딩을 시도한다.
만약, 자막 파일이 utf-8로 인코딩된 파일이였다면 문제없이 읽혔을 것이다.

> 즉, 종합해보면 자막 파일이 utf-8이 아니라 다른 한글 인코딩인 것이다!

한글 인코딩의 역사는 [복잡](https://d2.naver.com/helloworld/19187)하지만 일단 쉽게 생각하면 `utf-8` 아니면 `euc-kr`이다.
그러니, `utf-8`이 아닌 `euc-kr`로 다시 파일을 open 해보자.
그러면, `open` 함수가 `euc-kr` 코덱을 사용해서 디코딩(decoding)할 것이다.

~~~python
with open("cheeze.smi", "r", encoding='euc-kr') as f:
    print(f.readlines())  # 성공!
~~~

**성공!**

한글 인코딩 2가지만 기억하자.

> 한글파일(웹페이지)는 왠만하면 utf-8 아니면 euc-kr로 인코딩 되어있다!


## 참고글

- [한글 인코딩의 역사와 유니코드](https://d2.naver.com/helloworld/19187)
