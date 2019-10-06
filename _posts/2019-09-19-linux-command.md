---
layout: post
title:  "Linux 명령어 모음 (1)"
date:   2019-09-19 10:00:00 +0900
categories: Linux, command
---

로그인 가능 개수는 7개.

`ctrl+alt+F1`: 그래픽으로 보여지는 로그인 기능

패스워드는 MFA 로 암호화되어 있음.

1. gcc
2. vi
3. gdb

`enter`키 칠 때마다 한 줄씩 나오는 걸 **prompt** 라고 함!

`cursor`

악세서리: xeyes, xterm,


---

**shell!!!!**터미널 하나를 띄우면 shell이 자동적으로 동작한다!
echo $Shell: 셀 확인 가능

셀은 기능이 3가지가 있다.

1. user machine interface
2. 명령어 실행 -> 결과 보여줌
3. programming language

bash: born again shell
sh: bourne shell
csh, kcsh, tcsh

근데 bash랑 sh를 많이 씀.

shell에서 빠져나오기! -> `exit` or `ctrl+d`

-붙으면 옵션 param, 없으면 argv, --면 옵션 param이 없는 경우.

ex) `cmd -p1 -p2 -p3 arg1 arg2`

## 특수문자! 중요함!
1. 대소문자 구분할 것!
2. space!!로 구분함!

## Shell이 하는 일! 중요함

1. 명령어 하나씩 하나씩 line -> parsing (parser)
2. cmd file 존재 여부
3. cmd file 로딩 (어디에? 메모리에!) -> 그 다음 execution
4. control이 return to shell!
5. 이제 프롬포트가 떨어진다!


## Directory

- `cd` -> home directory로 이동! (home은 화면 켰을 때의 위치)
- `cd /`, `pwd`(play working directory)
- `cd ..` **..: current dir file file인 점을 명심!**
- `cd .` **.: upper dir file**

directory path
1. `absolute path`: /../../../ (절대경로)
2. `relative path`: ../ (상대경로)

### home으로 이동하는 방법
1. cd /home/~
2. cd ~ID
3. cd $HOME
4. cd ~
5. cd

`tty`: 터미널 번호를 알 수 있음!
`mnt`: cd 홈

## ls
- `ls -a` .file: 닷 파일이라고 부름!
- `ls -F` /붙으면 디렉토리
- `ls -s` 파일의 크기를 알려준다! 그 값에 1024 byte를 곱하라! (1024 = 1block)
    -  character device
    -  block device -> 속도가 빠른 곳에서 쓰인다!
- `ls -l`
- `ls -al`
    - permission -> owner -> size -> 수정 날짜
    - d은 디렉토리 -는 파일
    - r: read, w: write, x: exe (permission mode)
    - 3개씩! owner / group / others
    - permission에서 -: unset.
    - ex) rw-r-xr--: 654 -> `chmod`

## touch
1. 빈 파일 만들기
2. **time update**

## dir
`mkdir`: 디렉토리 만들기
`rmdir`: 디렉토리 제거 (단, 빈 디렉토리 일 경우!)

## mv

## rm

rm C/A
ls C

rm file삭제고
rmdir 디렉토리

**옵션 param은 붙여 쓸 수 있지만 arg을 동반한 옵션 param 은 붙여서 사용하지 못한다**
