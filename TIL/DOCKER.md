# Docker



### 도커 기본 명령어

실행

````bash
docker run
````

컨테이너 목록 확인 

````
docker ps
````

이미지 목록 확인하기

````bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
````

이미지 다운로드하기 

````
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
````

이미지 삭제

````
docker rmi [OPTIONS] IMAGE [IMAGE...]
````

컨테이너 명령어 실행

````bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
````



옵션

| 옵션  |                                             |
| ----- | ------------------------------------------- |
| -d    | detached mode. 백그라운드 모드              |
| -p    | 호스트와 컨테이너의 포트를 연결(포워딩)     |
| -v    | 호스트와 컨테이너의 디렉토리를 연결(마운트) |
| -e    | 컨테이너 내에서 사용할 환경변수 설정        |
| -name | 컨테이너 이름 설정                          |
| -rm   | 프로세스 종료시 컨테이너 자동 제거          |
| -it   | 터미널 입력을 위한 옵션                     |
| -link | 컨테이너 연결                               |

