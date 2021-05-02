# Tomcat

### 설치

: 아파치페이지에서 설치하거나 docker 혹은 homebrew에서 설치 (나는 homebrew)



**homebrew 설치시**

/usr/local/Cellar/ 내부에 tomcat이 설치되어 있고, 설치된 파일 bin 경로에서 실행

1) 해당 파일 경로로 이동

````bash
cd /usr/local/Cellar/tomcat@9/9.0.44/bin 
````

2) 실행

````bash
./catalina start
````

3) 종료

````bash
./catalina stop
````

* 작업이 끝난 뒤 반드시 종료해준다.





**이클립스와 연동, 실행**

이클립스에서 web 프로젝트 사용 시, 톰캣을 연동해서 사용. 

homebrew를 통해 tomcat설치 후 연동 시, 해당 경로를 반드시 아래의 경로로 지정한다.(libexec)

````bash
bin % cd /usr/local/Cellar/tomcat@9/9.0.44/libexec
````



* 이클립스에서 run시, 이클립스 자바 내장 브라우저가 실행. 자바 브라우저가 아닌 다른 웹(자신의 서버나 크롬)에서 확인하고 싶을 시, server 변경을 해줘야 한다. chrome의 경우 해당 파일이 설치된 경로를 입력해주면 된다. 



연동시, 

default file에 build/classes 필수 -> next -> WebContent 파일 입력. 



### 오류

가장 자주 발생하는 오류는 서버포트를 찾을 수 없다는 오류. 나의 경우 원인은 서버 충돌이었고, 이 문제는 오라클을 사용하게 되면서 나타났다. 이 경우 해결법은 다음과 같다. 

(혹은 외에, Tomcat 프로세스가 실행된 채로 남아있게 될 경우 역시 서버가 충돌되어 같은 오류가 발생한다.)



1) 해당 8080포트 찾기

````bash
sudo lsof -i :8080
````

* 위의 명령어로 검색하면 PID값을 볼 수 있다.



2) 해당 포트 죽이기

````bash
kill -9 (PID 값)
````



이후 다시 실행해보면 8080포트는 다시 잘 열리는 것을 확인할 수 있다.



* 하지만 위와 같은 해결은 일시적일 뿐, 바보같은 짓이다. 결국 DB와 tomcat 모두 사용하게 되는데, 그 경우 두 포트는 충돌이 나기 때문에 한 쪽은 사용하지 못하게 되기 때문. 따라서 결국에는 포트 하나의 값을 변경해준다.



docker의 경우: 

​	해당 컨테이너의 포트를 삭제하고 다시 변경하는 것은 아직 잘 모르겠다. 그러나 포트를 새로 추가한 새로운 컨테이너를 생성하는 방법은 다음과 같다

````bash
	docker run -p 9090:9090 jaspeen/oracle-xe-11g:latest
````



하지만 그냥 tomcat Connect 포트를 변경해주는 게 빠르다. 

해당 파일 server.xml에서 

Connector - port의 값을 변경해주면 된다. (8080->9090으로 변경함)