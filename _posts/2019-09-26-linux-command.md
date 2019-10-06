---
layout: post
title:  "Linux 명령어 모음 (2)"
date:   2019-09-26 10:00:00 +0900
categories: Linux, command
---

# 리눅스 프로그래밍

## rm 명령어

`rm`: 파일 지우기
`rm a`: a파일 지우기
`rm a b c`: a, b, c파일 지우기
`touch aa bb a b a1a b1b`
`rm a*`: a로 시작하는 파일을 다 지운다.
`rm ?1?`: b1b파일이 지워진다.
- *: 어떤 문자가 나오든지! (any char, any len (0포함)) (`touch a`를 하고 `rm a*`해도 a파일 지워짐)
- ?: any char but only one char!
`rm -i *`: **-i**는 iterator 즉, 지울 것인지 안지울 것인지 확인하는 명령어. verbose mode라고 부름.


`mkdir B`: 하고 `cd *`하면 B 디렉토리 들어가나,,, 여러 디렉토리 있으면 이 명령어는 안먹힘.

`rmdir`:은 비워있지 않은 디렉토리는 못 지움.

`rm -fr A`: A디렉토리를 강제로 recursive하게 지워라
- `f`: **force**
- `r`: **recursive** -> 프로그램의 제어를 반복하는 명령부호 재귀반복.

##  cp

`cp`: file copy
`cp /etc/passwd ./. or .`
`cp ./passwd pa`
`cp /bin/cp cp`
`ps -a > prstat`: ps -a의 명령어 값이 prstat라는 파일로 들어간다!

## 파일 내용 보기 - cat이 기본!

`head [file]`: 파일의 앞 부분의 10줄을 보여 준다.
`head p*`: p로 시작하는 파일의 앞 부분 10줄을 보여 준다.
`tail [file]`: file의 끝 부분 10줄을 보여 준다.
`cat [file]`: file의 모든 내용을 다 보여 준다. (catch의 약자)
`more [file]`: 한 페이지가 전체 몇 페이지 보여주냐!(**표준은 25줄**)
- `enter`: **one line 씩**
- `space`: **one page 씩**
- `q`: quit의 약자로 빠져나옴.

> less 보다 more 명령어를 더 많이 사용한다.

**굉장히 많이 쓰는 명령어!**

`cat < pa`: pa라는 파일을 (**redirection**)
`cat pa`
`cat pa > /dev/null`: pa라는 파일을 null(black hole) 로 보냄!

**>**: 출력을 redirection.
**<**: 입력을 redirection.

`cat > catout`: 막 치고 ctrl+c or d 하면 입력한 값이 파일로 저장됨.

`ls > catout`: ls의 값을 catout 파일에 저장한다.

`ps -u >> catout`: **>>**은 본래 파일에서 append한다!!
- `>>`: append 해주는 명령어!
- `>`: 원래 파일에다가 덮어 쓰기한다.

`more pa`
- `root`: login name
- `:`: 구분자 (딜리미터 delimeter)
    - 구분자 한 줄: **record**
    - 구분자 하나의 단어 단어: **field**
    - 전체 record: **table**
- `x`: password
- `0`: user id. (uid)
- `0`: group id.
- `/root`: home directory 위치
- `/bin/bash`: login 통과하면 쉘을 뭘 실행시킬지!

- 일반 uid는 1000번.

## Process

`top`
    - pid: process id
    - pr: 우선순위
    - ni: nice값 --> pr을 관리하는 값
    - s: status
    - zombie: 죽여도 죽여도 생성되는 것. 있다면 불안정한 kernel이다.


`ps`: process status
    - ps 두번 동작하면? 각각의 프로세스가 부여되면서 값이 다르게 나온다.
    - `-u`: user process (gnome: graphic 관련)
    - `-ux`: background process도 볼 수 있음.
    - `-a`: system process 볼 수 있음.
    - `-ax`: 이 명령어는 다 볼 수 있음. + []는 데몬 관련
    -

**daemon**: 벡그라운드에서 유지 보수 해주는 process.

`sol`, `gnome-mahjongg`

`jobs`: background task 보기!!
`bg %1`
`fg %2`
^z
`kill %1`: background에 1번 job을 kill한다.
`sol &`: fb -> bg로 이동하는 명령어!

shell!!!
foreground 오직 1개만 running 가능
background n개 running 가능

## 명령어 line

`ps -ax`:
`ps -ax | more`:
    - **|**의 역할: ps -ax의 출력이 more의 입력으로 들어간다!
    - **;**의 역할: enter키와 똑같다! **잘 기억해놓을 것!**

`top; sol; ls -a`: top -> sol -> ls -a 차례대로 !
or
`top; ps -u; ls -a`: top -> sol -> ls -a 차례대로 !

`control + w`: space바 기준 지운다.
`control + u`: 하나의 라인을 지운다.

## history

`history`: 내가 친 명령어 recall
`!!`: 직전 명령어 반복
`!숫자`: 명령어 list에서 해당 번호 recall
`!(string)`: 명령어 list에서 가장 최근 string으로 시작하는 명령어 recall
`!!:숫자`
`^string1^string2`

cmd는 다 자리의 값이 정해져 있다.

`$0 $1 $2 $3 ...`이런 순서로 정해져 있다.
$*: parameter list
$#: parameter 개수

shell: argc!
c: argv!

`ls -a` -> `ps !!:1`을 하면 **-a**라는 arg를 가져온다!!!! 즉, `ps -a`명령어가 실행됨!

^string1^string2 -> `ls -a`-> `^a^Fs`하면 `ls -Fs`로 명령어가 쳐진다.
