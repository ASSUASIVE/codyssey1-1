# 프로젝트 개요(미션 목표 요약)

# 실행 환경(OS/쉘/터미널, Docker 버전, Git 버전)

# 수행 항목 체크리스트(터미널/권한/Dockerfile/포트/볼륨/Git/GitHub)

# 검증 방법(어떤 명령으로 무엇을 확인했는지) + 결과 위치 링크

# 트러블슈팅 2건 이상(문제 -> 원인 가설 -> 확인 -> 해결/대안)

# 기술 문서만읽어도 전체 수행 내용을 파악할 수 있어야 한다.

## 1) 실행 환경
- OS: Windows 11
- Shell: PowerShell (VS Code Integration Terminal)
- Docker: 29.9.2
- Git: 2.56.0

## 2) 수행 체크리스트
- [ ] Git 설정 + GitHub 연동
- [x] 터미널 기본 조작 및 폴더 구성
- [x] Docker 설치/점검
- [x] hello-world 실행
- [x] Docker 기본 운영 명령(images/ps/logs/stats/etc..)
- [x] 권한 변경 실습
- [ ] ubuntu 컨테이너 실행 및 내부 진입
- [ ] Dockerfile 빌드/실행
- [ ] 포트 매핑 접속
- [ ] 바인드 마운트 반영
- [ ] 볼륨 영속성
- [ ] Git 설정 + GitHub 연동

## 3) 수행 로그(발췌)

### Git 설정 + GitHub 연동




### 터미널 기본 조작 및 폴더 구성

#### 지금 내 위치 확인

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> pwd

Path                                                   
----                                                   
C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments
```

#### 파일/폴더 목록 보기

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> ls


    디렉터리: C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments


Mode                 LastWriteTime         Length Name                                                                  
----                 -------------         ------ ----                                                                                                                              
-a----      2026-11-04   오후 1:30          11049 README.md                                                             
```

##### 파일/폴더 목록 보기(숨김 포함)

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> ls -Force


    디렉터리: C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments


Mode                 LastWriteTime         Length Name                                                                  
----                 -------------         ------ ----                                                                                                                               
-a----      2026-11-04   오후 1:30          11049 README.md                                                             
```

#### 폴더 안으로 이동

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey> cd 1_1_assignments
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> 
```

#### 상위 폴더로 나가기

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> cd ..
PS C:\Users\ethanhaeunc4031\Ethan-codyssey> 
```

#### 생성

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> New-Item 

cmdlet New-Item(명령 파이프라인 위치 1)
다음 매개 변수에 대한 값을 제공하십시오.
Path[0]: test-copy.txt
Path[1]: 


    디렉터리: C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments


Mode                 LastWriteTime         Length Name                                                                  
----                 -------------         ------ ----                                                                  
-a----      2026-11-04   오후 3:16              0 test-copy.txt
```

#### 생성2

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> New-Item -Name "test-copy.txt" -ItemType File


    디렉터리: C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments


Mode                 LastWriteTime         Length Name                                                                  
----                 -------------         ------ ----                                                                  
-a----      2026-11-04   오후 3:18              0 test-copy.txt   
```





### 권한 변경 실습 *** 처음부터 다시 하기, docker가지고 파일 생성 등 로그 작성 ***

#### 대상/변경 전/변경 후/숫자

```
test.txt -rw-r--r-- -rwxrwxrwx 644->777
testdir drwxr-xr-x drwx------ 755->700
```

#### 사용한 명령어

```
chmod 777 testfile.txt
chmod 700 testdir
```

변경 전

```
root@cfb0165a6481:/app# ls -l
total 12
-rwxrwxrwx 1 root root 11049 Nov  4 04:30 README.md
-rw-r--r-- 1 root root     0 Nov  4 04:46 test.txt
drwxr-xr-x 1 root root  4096 Nov  4 04:46 testdir
```

변경 후

```
root@cfb0165a6481:/app# chmod 777 test.txt
root@cfb0165a6481:/app# chmod 700 testdir
root@cfb0165a6481:/app# ls -l
total 12
-rwxrwxrwx 1 root root 11049 Nov  4 04:30 README.md
-rwxrwxrwx 1 root root     0 Nov  4 04:46 test.txt
drwx------ 1 root root  4096 Nov  4 04:46 testdir
```

### Docker 설치 및 점검

#### docker version

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker --version
Docker version 29.9.2, build a82e528
```

#### docker info

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker info
Client:
 Version:    29.9.2
 Context:    desktop-linux
 Debug Mode: false
 Plugins:
  agent: Docker AI Agent Runner (Docker Inc.)
    Version:  v1.152.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-agent.exe
  ai: Docker AI Agent - Ask Gordon (Docker Inc.)
    Version:  v1.33.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-ai.exe
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.38.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-buildx.exe
  compose: Docker Compose (Docker Inc.)
    Version:  v5.6.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-compose.exe
  debug: Get a shell into any image or container (Docker Inc.)
    Version:  0.49.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-debug.exe
  desktop: Docker Desktop commands (Docker Inc.)
    Version:  4.97.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-desktop.exe
  dhi: CLI for managing Docker Hardened Images (Docker Inc.)
    Version:  v0.0.9
    Path:     C:\Program Files\Docker\cli-plugins\docker-dhi.exe
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.32
    Path:     C:\Program Files\Docker\cli-plugins\docker-extension.exe
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v1.4.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-init.exe
  mcp: Docker MCP Plugin (Docker Inc.)
    Version:  v0.44.2
    Path:     C:\Program Files\Docker\cli-plugins\docker-mcp.exe
  model: Docker Model Runner (Docker Inc.)
    Version:  v1.2.9
    Path:     C:\Program Files\Docker\cli-plugins\docker-model.exe
  offload: Docker Offload (Docker Inc.)
    Version:  v0.7.21
    Path:     C:\Program Files\Docker\cli-plugins\docker-offload.exe
  pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
    Version:  v0.3.2
    Path:     C:\Program Files\Docker\cli-plugins\docker-pass.exe
  sandbox: "docker sandbox" is deprecated, use Docker Sandboxes instead (Docker Inc.)
    Version:  v0.13.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-sandbox.exe
  scout: Docker Scout (Docker Inc.)
    Version:  v1.27.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-scout.exe

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 1
 Server Version: 29.9.2
 Storage Driver: overlayfs
  driver-type: io.containerd.snapshotter.v1
 Logging Driver: local
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Discovered Devices:
  cdi: docker.com/gpu=webgpu
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 nvidia runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: b7a25261e029d68978bbf290df0a62fc819b3c51
 runc version: v1.5.2-0-g29dd3dc2
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.18.54.1-microsoft-standard-WSL2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 24
 Total Memory: 15.25GiB
 Name: docker-desktop
 ID: 00ac1422-4e54-4feb-a91a-d0196885130e
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Labels:
  com.docker.desktop.address=npipe://\\.\pipe\docker_cli
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5555
  127.0.0.0/8
  ::1/128
 Live Restore Enabled: false
 Firewall Backend: iptables
 ```

##### Docker 실행

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker run -it --rm -v "${PWD}:/app" -w /app python:3.12-slim bash
root@f0c7d99b2ada:/app# 
```

### hello-world 실행

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
d5e71e642bf5: Download complete 
Digest: sha256:c567b231f65614688711a75f31518a064258a51d442117a3e771a3a8fdba78ef
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
### Docker 기본 운영 명령(images/ps/logs/stats/etc..)

#### images
```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker images
                                                                                                    i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c567b231f656       25.9kB         9.49kB    U   
python:3.12-slim     b18b261e1b49        180MB         45.5MB 
```

#### ps

##### 실행 중인 컨테이너만
```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

##### 종료된 것 포함 전체
```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
5e91d81ea406   hello-world   "/hello"   50 seconds ago   Exited (0) 49 seconds ago             suspicious_benz
```

#### logs

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker logs suspicious_benz

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

#### stats

```
PS C:\Users\ethanhaeunc4031\Ethan-codyssey\1_1_assignments> docker stats
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS
```
> N/A(실행 중인 컨테이너 없음)

#### etc..



##### 








# 트러블슈팅 2건 이상(문제 -> 원인 가설 -> 확인 -> 해결/대안)

## 트러플슈팅 1: txt 파일 한글 깨짐
- 문제: test.txt 생성 후 파일 내에 한글로 되어있는 text가 깨져 보임
- 원인 가설: 파일 인코딩 불일치(CP949 <-> UTF-8)
- 확인: VSCode 상태바에서 인코딩 확인
- 해결: "Reopen with Encoding"으로 올바른 인코딩 선택