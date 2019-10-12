---
layout: post
title: "Framework와 Library의 차이"
date: 2018-08-04 10:00:00 +0900
tas: [study, interview]
comments: true
---

Framework와 Library를 구분하려면 **제어(control)**[^1]가 어느 쪽에 있는지 생각해보면 된다.


Framework(대표적으로 Flask)는 제어의 흐름(flow of control)이 Framework(Flask) 쪽에 있다.
즉, 내가 쓸 Framework를 선택하면 나는 그 Framework의 코드와 디자인 방식을 따라야 한다.
Framework는 나에게 hook[^2]이나 callback[^3]같은 것들을 제공할 것이고 Framework가 원하는 코드로 작성해야 한다.

- Framework의 예
  * [Ruby on Rails](https://rubyonrails.org/)
  * [Django](https://www.djangoproject.com/)
  * [Flask](http://flask.pocoo.org/)


Library는 제어가 나에게 존재한다.
(Library는 objects/functions/methods의 집합체) 그렇기에 Library에 있는 코드를 내가 원하는 코드로 작성할 수 있다.
마치 많은 재료(functions)를 가지고 다양한 종류의 음식(program)을 만드는 것과 비슷하다.

- Library의 예
  * [Requests](http://docs.python-requests.org/en/master/)
  * [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)


## Library-Framework-Code's relation
![Library, Framework and your Code]({{ "/../../data/frameVSlibrary.jpg" }})


## 참고자료

- [What's difference between a library and a framework?](https://www.quora.com/Whats-the-difference-between-a-library-and-a-framework)
- [What is the difference between a framework and a library?](https://stackoverflow.com/questions/148747/what-is-the-difference-between-a-framework-and-a-library)


***
[^1]: Inversion of control. (제어의 역전) 제어가 '나'에게 있는 게 아니라 '프레임웍'으로 '역전'되어있다는 뜻이다. (즉, 제어가 자신에게 있는 게 정상적인 상황이라 생각하면 프레임웍이 제어를 가진 건 '역전'되었다고 이해할 수 있다.)
[^2]: Hook. 일단은 callback 같은 것으로 이해하자.
[^3]: Callback. A라는 함수를 call 한 뒤에 반드시 B 함수를 call 하도록 할 때, B를 A의 callback 함수라 한다. 우리가 일상에서 전화를 못 받을 때 '콜백해줘~'할 때 쓰는 그 callback이다.
