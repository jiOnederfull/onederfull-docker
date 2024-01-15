# onederfull-docker
## How to Install
- Mac: https://docs.docker.com/desktop/install/mac-install/

## Docker Image & Container
### image: 컨테이너를 생성할 때 필요한 요소, 컨테이너를 생성하고 실행할 때 읽기 전용으로 사용
- 여러 개의 계층으로 된 바이너리 파일로 존재
- `저장소 이름/이미지 이름:이미지 버전(태그)` 라고 설명되어 있는데 본인이 이해하기에는
- `(도커 허브 계정 이름)/저장소 이름:태그`의 구성에서 `(도커 허브 계정 이름)/저장소 이름` == `repository` / `저장소 이름:태그` == `image` 로 이해하는게 나은 것 같음

- 그렇지 않으면 밑의 그림에서 REPOSITORY에 ubuntu가 적혀있고, IMAGE에 ubuntu:0.0가 적혀있는 것이 이해가 잘 가지 않음
   <img width="740" alt="image" src="https://github.com/jiOnederfull/onederfull-docker/assets/48719289/809f4726-45a0-4241-b03c-f59a64ab0a94">
- 실제로 도커 이미지를 빌드할 때도, `이미지 이름:이미지 버전`이 아니라, `저장소 이름:태그`로 빌드해서 `저장소 이름:태그`가 `이미지 이름이다`로 이해하는게 훨씬 이해가 쉬움

### container: 이미지로부터 생성, 독립된 공간
- 한 컨테이너에서 일어난 일은 그 컨테이너를 생성한 이미지, 같은 이미지로부터 생성된 다른 컨테이너, 컨테이너가 생성되어있는 호스트에 반영되지 않음

## 컨테이너를 외부에 노출
- 컨테이너는 가상 IP 주소를 할당받음
- `172.17.0.x`의 IP를 순차적으로 할당
- `eth0` - 도커의 NAT IP를 할당받은 인터페이스
- `lo` - 로컬 호스트 인터페이스
- 기본 설정으로는 외부에서 컨테이너에 접근할 수 없고, 도커가 설치된 호스트에서만 접근 가능
- 외부에 컨테이너의 애플리케이션을 노출하기 위해서는 eth0의 IP와 포트를 호스트의 IP와 포트에 바인딩해야 함


## Docker Command
### `docker run`
- 컨테이너 생성하고 실행, 로컬 도커 엔진에 이미지가 존재하지 않을 경우 자동으로 docker pull
- `pull` + `create` + `start` + `attach`(`-i -t` 옵션 사용했을 때)
- option
  - `-i -t`: 컨테이너와 상호(interactive) 입출력 가능
  - `-p (컨테이너 외부 포트):(컨테이너 내부 포트)`: 컨테이너의 포트와 호스트의 포트 바인딩
  - `--detach / -d`: 백그라운드 실행
  - `--restart=always`: [자동 재시작](https://docs.docker.com/engine/reference/commandline/run/#restart)
  - `--rm`: 컨테이너 중단시 삭제

### `docker pull`
- 이미지 내려받기

### `docker images`
- 이미지 목록

### `docker create`
- 컨테이너 생성(만), 로컬 도커 엔진에 이미지가 존재하지 않을 경우 자동으로 docker pull
- `pull` + `create`
- create 명령어의 결과로 출력된 무작위의 16진수 해시값은 **컨테이너의 고유 ID**
- option
   - `-i -t`: 컨테이너와 상호(interactive) 입출력 가능
   - `--name`: 컨테이너 이름 설정

### `docker start`
- 컨테이너 실행

### `docker attach`
- 컨테이너 내부로 들어감

### `docker ps`
- 동작중인 컨테이너 목록
- option
   - `-a`: 정지된 컨테이너 포함 모든 컨테이너
   - `-q`: 컨테이너 ID만 출력
- example
   - `docker ps --format "table {{.ID}}\t{{.Status}}\t{{.Image}}"` # go 템플릿

### `docker inspect`
- 컨테이너 정보 확인

### `docker rename`
- 컨테이너명 변경

### `docker rm`
- 컨테이너 삭제
- option
   - `-f`: 실행 중인 컨테이너 강제 삭제
- example
   - `docker rm $(docker ps -a -q)` # 모든 컨테이너 삭제
 
### `docker container prune`
- 모든 컨테이너 삭제
 

### `docker stop`
- 컨테이너 정지
- example
   - `docker stop $(docker ps -a -q)` # 모든 컨테이너 정지



- `Ctrl + D`: 컨테이너를 종료하고 빠져나옴
- `Ctrl + P, Q`: 컨테이너를 종료하지 않고 빠져나옴

## Question
- ~~docker create과 docker run의 차이는?~~
- 자체적으로 만든 이미지가 존재할 때 Image 이름과 Tag 가 같으면 새로운 이미지를 만드나? 아니면 기존 이미지가 있다고 판단하고 안 만드나? (base upgrade)
- image id 생성 기준



- docker container 내부 유저 지정 방법
- Running a Docker container as a non-root user
https://medium.com/redbubble/running-a-docker-container-as-a-non-root-user-7d2e00f8ee15

- https://docs.docker.com/compose/compose-file/07-volumes/
