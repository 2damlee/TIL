# HTML

> html5는 html tag + css + javascript를 모두 포함하는 표준 규격을 갖고 있다.



### TAG



**태그 축약** 

| 글자표현         | h1-h6<br />p br hr                            |
| ---------------- | --------------------------------------------- |
| **링크**         | **a**                                         |
| **목록**         | **ul   ol   li**                              |
| **표**           | **table   tr   th   td**                      |
| **화면영역표시** | **div   span**                                |
| **시맨틱**       | **header   nav   section   article   footer** |
| **입력양식**     | **form   input   textarea   select   option** |
| **멀티미디어**   | **img   audio   video**                       |



#### 1) 구성

````html
<html>
  <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    
    <!--출력 내용
    
  </body>
</html>
````



#### 2) 글자크기

````html
<h1 id="here"> k digital 과정 </h1> 
<h3> web client 과정 </h3>
<h5> html 태그 </h5>
<p>현재 우리는 html 태그 가운데 &nbsp; &nbsp; &nbsp; 글자크기와 관련된 태그 출력
<br>
	<i>기울임</i> 
  <b>굵게</b>
  <small>작게작게</small>
<br>  
<p> <!-- <p>는 일종의 본문  
````

​	* id는 어디든 작성 가능하다. 해당 태그의 이름을 지정해주는 역할



#### 3) 링크 이동

````html
<a href="http://www.multicampus.co.kr"> 다른 페이지로 이동 </a><br>

<a href="주소이름"> 현재 서버의 현재프로젝트의 first.html로 이동 </a><br>
<a href="/프로젝트명/first.html"> 현재서버의 다른 프로젝트의 first.html 이동 </a><br>
<a href ="#here"> 현재파일의 첫부분 이동 </a><br><!-- id가 here인 곳으로 이동
````



#### 4) List

````html
<!-- 순서 배열 -->
<ol type="a"> <!-- 타입 지정 가능  -->
    <li>자바</li>
    <li>sql</li>
    <li>spring</li>
    <li>jquery</li>
    <li>jsp</li>
</ol>
<!-- 순서 없는 배열 -->
<ul type="square">
    <li>자바</li>
    <li>sql</li>
    <li>spring</li>
    <li>jquery</li>
    <li>jsp</li>
</ul>
````



#### 5) Table

````html
<h1>테이블 tag</h1>
    <table border="3"> 
        <tr><th>사번</th><th>이름</th><th>급여</th></tr>
        <tr><td>1행 1열 데이터</td><td>1행 2열 데이터</td><td>1행 3열 데이터</td></tr> 
      <!-- td는 table data th는 table head -->
        <tr><td>2행 1열 데이터</td><td>2행 2열 데이터</td><td>2행 3열 데이터</td></tr>
        <tr><td>3행 1열 데이터</td><td>3행 2열 데이터</td><td>3행 3열 데이터</td></tr>
    </table>

<!-- 행 합치기 (rowspan) -->
		<table border="3"> 
        <caption> 로그인 테이블 </caption>
        <tr><td>로그인아이디입력</td><td>xxxxx</td><td rowspan="2">로그인버튼</td></tr> 
        <tr><td>암호입력</td><td>xxxxx</td><td>
   
    </table>
  
<!-- 행 합치기 (colspan) -->
		<table border="3"> 
        <caption> 로그인 테이블2 </caption>
        <tr><td>로그인아이디입력</td><td>xxxxx</td></tr> 
        <tr><td>암호입력</td><td>xxxxx</td><td>
        <tr><td colspan="2">로그인버튼</td></tr>    
    </table>
````



#### 6) 미디어 삽입

````html
<h1>이미지 보여주기</h1>
        <img src = "https://cdn.webshopapp.com/shops/30495/files/156411065/monsterapertusum-				hole-plant.jpg"  alt="이미지가 이동되었습니다 .. " width="200"><br>
	<!-- 온라인 이미지 주소 사용 가능, 보존가능성 X 
	alt는 이미지를 부가설명 -->
        <img src = "images/html5.jpg" width="200"><br> 
	<!--이미지 직접 삽입 시, 해당 파일이 반드시 프로젝트 폴더 내에 위치해야 함-->

        <img src = "/html/images/html5.jpg"><br> 
        <img src = "http://127.0.0.1:5500/multimedia.html/images/html5.jpg"><br>

        <h1>오디오 들려주기</h1>
        <audio src="multimedia/old_pop.mp3" controls="controls"></audio>

        <h1>비디오 보여주기</h1>
        <video src="multimedia/Wildlife.mp4"
         controls="controls" poster="images/chrome.jpg" width="500"></video>
	<!-- control은 재생 버튼
````



#### 7) div와 span

````html
<div style="color: rgb(124, 125, 162);"> 
     <h1>div 태그 - block 형식</h1>
     <h3> div 태그 - block 형식</h3>
     <h5>div 태그 - block 형식</h5>
    </div>
        <!-- <br> 사용하지 않아도 줄바꿈이 가능하다 : div, h1-h6, p, ul, ol, table: block 양식 표현(나머				지는 줄바꿈이 되지 않음, <br>태그 필요)
        공간분할: div 합쳐서 두고, 여러 군데 색 지정 가능
        br을 사용하지 않아도 줄바꿈을 가지면서도 공간을 분할
        여러 태그를 묶어서 한 영역으로 분리할 때, div 태그를 사용
    
        <div>프로그램 진행 중 내용 변경 추가 .. 영역을 확보 .. (java script)</div>-->

        <span> <h1 style="background-color: darkseagreen;">div 태그 - block 형식</h1> </span>
        <span> <h3 style="background-color: darkslateblue;"> div 태그 - block 형식</h3> </span>
        <span> <h5 style="background-color: gray;">div 태그 - block 형식</h5> </span>
        <!--썼던 내용만큼만 크기를 정해줌 그 다음 태그는 오른쪽에 추가하는 형식, 같은 라인을 쓴다.
            공간분할을 Inline 방식으로-->
````





### 8) form



**input**

* form action / input type= "text", "submit", "password", "hidden"

````html
<form action="loginprocess"> 
<!--submit타입의 버튼을 누르면, "loginprocess"로 값(value)을 전달-->
  
아이디 입력: <input type="text" name="id"><br> <!-- name은 이름지정과 같은 것-->
<input type=submit value="로그인"> <!--submit 버튼은 입력값을 form action에 전송하는 기능-->

암호 입력: <input type="password" name="pw"><br>
권한 입력:  <input type="hidden" name="role" value="admin"><br> 
  <!--hiden은 입력값을 받지 않는데 admin이란 타입을 반드시 전송-->
  
````

* input type= "radio", "checkbox"

````html
성별:  <input type="radio" name="gender" value="male"> 남자 
		 	<input type="radio" name="gender" value="female"> 여자<br> 
  		<!--radio : 단 하나의 값만 선택 가능-->

수강과목: <input type="checkbox" name="subject" value="java"> 자바
        <input type="checkbox" name="subject" value="oracle"> 오라클
        <input type="checkbox" name="subject" value="html"> html
        <input type="checkbox" name="subject" value="jsp"> jsp<br>
			<!-- 복수 선택 가능, 동일 변수명에 여러 값 가능 -->   
````

* input type="file", "textarea"

````html
 <input type="file" name="myfile"><br>
<!-- 파일 삽입이 가능 -->

<textarea rows = "5" cols="100"></textarea><br>
<!--여러 줄의 text 가능, 입력은 무한 가능 처음 보여지는 것은 5줄까지. 그 다음부터는 스크롤바-->

````

* input type="select"

````html
<!--옵션 선택할 때-->
<select>
  <option> 라면 </option>
  <option> 떡볶이 </option>
</select>

<!--복수 옵션 선택할 때-->
<select multiple="multiple">
  <optgroup label="분식">
  <option> 라면 </option>
  <option> 떡볶이 </option>
  </optgroup>
  <optgroup label="일식">]
  <option> 일식 </option>
  <option> 우럭 </option>
  <option> 짬뽕 </option>
  <option> 사케동 </option>
  </optgroup>
  </select> 
````

* input type="submit", "reset", "button"

````html
<input type="button" value="기능?"><br>
<!--자바스크립트로 기능을 정할 수 있음-->

<input type=reset value=입력취소><br>
<!--선택 항목들이 초기화-->

<input type=submit value="로그인">
<!--submit 버튼은 입력값을 form action에 전송-->
````



#### 9)Sementic

````html
<html>
    <head>
        <meta charset="UTF-8">
    </head>
    <body>
        <header>홈페이지 상단(로고 회사명)</header>
        <nav>메인메뉴 게시물리스트 글쓰기 글수정 글삭제</nav>
        <section>
            메인메뉴 한 개 작업 내용 - 게시물리스트(검색창, 게시물리스트테이블, 페이지번호)
            <article>검색창 작업</article><!-- 섹션의 부가적인 것이 아티클-->
            <article>게시물 리스트</article>
            <article>페이지 번호</article>
            </section>
        <footer>홈페이지 하단(잡다정보)</footer>
    </body>
</html>
<!--의미있는 태그들, 알아볼 수 있도록. 기능은 x, 약속된 방식으로 의미를 부여한 것 -->
````

