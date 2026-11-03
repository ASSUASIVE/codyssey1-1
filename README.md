# Ethan-codyssey
Github와 Codyssey 연동


## 프로젝트 개요(미션 목표 요약)

## 실행 환경(OS/쉘/터미널, Docker 버전, Git 버전)

## 수행 항목 체크리스트(터미널/권한/Dockerfile/포트/볼륨/Git/GitHub)

## 검증 방법(어떤 명령으로 무엇을 확인했는지) + 결과 위치 링크

## 트러블슈팅 2건 이상(문제 -> 원인 가설 -> 확인 -> 해결/대안)

## 기술 문서만읽어도 전체 수행 내용을 파악할 수 있어야 한다.

-----

## 1) 실행 환경
    - OS: Windows 11
    - Shell: PowerShell (VS Code Integration Terminal)
    - Docker: 29.9.2
    - Git: 2.56.0

## 2) 수행 체크리스트
    - [x] 터미널 기본 조작 및 폴더 구성
    - [x] 권한 변경 실습
    - [ ] Docker 설치/점검
    - [ ] hello-world 실행
    - [ ] Dockerfile 빌드/실행
    - [ ] 포트 매핑 접속(2회)
    - [ ] 바인드 마운트 반영
    - [ ] 볼륨 영속성
    - [ ] Git 설정 + VSCode GitHub 연동

## 3) 수행 로그(발췌)
권한 변경 실습

        대상/변경 전/변경 후/숫자

        testfile.txt -rw-r--r-- -rwxrwxrwx 644->777

        testdir drwxr-xr-x drwx------ 755->700

    사용한 명령어

        chmod 777 testfile.txt

        chmod 700 testdir

    변경 전

        root@31a402df5eba:/# ls -l

        total 56

        lrwxrwxrwx   1 root root    7 Apr 20  2026 bin -> usr/bin

        drwxr-xr-x   2 root root 4096 Apr 20  2026 boot

        drwxr-xr-x   5 root root  360 Nov  3 00:14 dev

        drwxr-xr-x   1 root root 4096 Nov  3 00:14 etc

        drwxr-xr-x   3 root root 4096 Oct 25 10:26 home

        lrwxrwxrwx   1 root root    7 Apr 20  2026 lib -> usr/lib

        lrwxrwxrwx   1 root root    9 Apr 20  2026 lib64 -> usr/lib64

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 media

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 mnt

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 opt

        dr-xr-xr-x 284 root root    0 Nov  3 00:14 proc

        drwx------   2 root root 4096 Oct 25 10:26 root

        drwxr-xr-x   4 root root 4096 Oct 25 10:26 run

        lrwxrwxrwx   1 root root    8 Apr 20  2026 sbin -> usr/sbin

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 srv

        dr-xr-xr-x  12 root root    0 Nov  3 00:16 sys

        drwxr-xr-x   2 root root 4096 Nov  3 00:16 testdir

        -rw-r--r--   1 root root    6 Nov  3 00:15 testfile.txt

        drwxrwxrwt   2 root root 4096 Oct 25 10:25 tmp

        drwxr-xr-x  12 root root 4096 Oct 25 10:24 usr

        drwxr-xr-x  11 root root 4096 Oct 25 10:26 var

    변경 후

        root@31a402df5eba:/# chmod 777 testfile.txt

        root@31a402df5eba:/# chmod 700 testdir

        root@31a402df5eba:/# ls -l

        total 56

        lrwxrwxrwx   1 root root    7 Apr 20  2026 bin -> usr/bin

        drwxr-xr-x   2 root root 4096 Apr 20  2026 boot

        drwxr-xr-x   5 root root  360 Nov  3 00:14 dev

        drwxr-xr-x   1 root root 4096 Nov  3 00:14 etc

        drwxr-xr-x   3 root root 4096 Oct 25 10:26 home

        lrwxrwxrwx   1 root root    7 Apr 20  2026 lib -> usr/lib

        lrwxrwxrwx   1 root root    9 Apr 20  2026 lib64 -> usr/lib64

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 media

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 mnt

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 opt

        dr-xr-xr-x 284 root root    0 Nov  3 00:14 proc

        drwx------   2 root root 4096 Oct 25 10:26 root

        drwxr-xr-x   4 root root 4096 Oct 25 10:26 run

        lrwxrwxrwx   1 root root    8 Apr 20  2026 sbin -> usr/sbin

        drwxr-xr-x   2 root root 4096 Oct 25 10:25 srv

        dr-xr-xr-x  12 root root    0 Nov  3 00:16 sys

        drwx------   2 root root 4096 Nov  3 00:16 testdir

        -rwxrwxrwx   1 root root    6 Nov  3 00:15 testfile.txt

        drwxrwxrwt   2 root root 4096 Oct 25 10:25 tmp

        drwxr-xr-x  12 root root 4096 Oct 25 10:24 usr

        drwxr-xr-x  11 root root 4096 Oct 25 10:26 var