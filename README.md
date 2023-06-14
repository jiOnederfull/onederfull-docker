# onederfull-docker
## How to Install
- Mac: https://docs.docker.com/desktop/install/mac-install/

## Docker Image & Container
### image: 컨테이너를 생성할 때 필요한 요소, 컨테이너를 생성하고 실행할 때 읽기 전용으로 사용
- `저장소 이름/이미지 이름:이미지 버전(태그)` 라고 설명되어 있는데 본인이 이해하기에는
- `(도커 허브 계정 이름)/저장소 이름:태그`의 구성에서 `(도커 허브 계정 이름)/저장소 이름` == repository / `저장소 이름:태그` == image 로 이해하는게 나은 것 같음

- 그렇지 않으면 밑의 그림에서 REPOSITORY에 ubuntu가 적혀있고, IMAGE에 ubuntu:0.0가 적혀있는 것이 이해가 잘 가지 않음
   <img width="740" alt="image" src="https://github.com/jiOnederfull/onederfull-docker/assets/48719289/809f4726-45a0-4241-b03c-f59a64ab0a94">
- 실제로 도커 이미지를 빌드할 때도, `이미지 이름:이미지 버전`이 아니라, `저장소 이름:태그`로 빌드해서 `저장소 이름:태그`가 이미지 이름이다로 이해하는게 훨씬 이해가 쉬움

### container: 이미지로부터 생성, 독립된 공간. 컨테이너에서 일어난 일은 이미지, 다른 컨테이너, 호스트에 반영되지 않음
