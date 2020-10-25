---
title: 만자로, 아치리눅스에서 ssh를 통한 X11forwarding 설정하기
tags: 터미널, 리눅스, x11, ssh
---

## server side
원격지가 우분투라면, 기본적으로 X11forwarding을 위한 설정이 완료되어있다. 하지만, 윈격지 서버가 우분투가 아니라면, 설정이 필요하다.

### xauth,  xhost 설치
cent의 경우

```bash
$ sudo yum install xauth
```

arch, manjaro의 경우

```bash
$ sudo pacman -S xorg-xauth xorg-xhost

```

### ssh 설정변경
먼저 원격지 서버로 접속한다.
```bash
$ ssh user@serverip -p 22
```
vi나 nano등을 사용해서, sshd_config 파일을 연다.
```bash
$ sudo vi /etc/ssh/sshd_config
```
다음 설정을 바꿔준다. #으로 주석처리가 되어있다면 이를 지워주면 된다.
```
X11Forwarding yes
X11UseLocalhost yes
AllowTcpForwarding yes
```
`:wq`로 저장한다.
### sshd를 재시작
cent의경우
```bash
$ sudo /etc/init.d/sshd reload
```
arch의 경우
```bash
$ systemctl restart sshd
```
이제 서버에서의 설정은 끝났다.
## client side
클라이언트에선 별다른 설정은 필요없다. ssh에 접속할때, -X 옵션을 추가하여 실행하면 된다.
