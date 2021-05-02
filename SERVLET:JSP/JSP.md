# JSP

css html등을 함께 써야 하고 응답하고 코드를 더 간단하게 쓰기 위해 등장. html태그를 작성하기 불편한 servlet의 단점을 보완, 응답 html 태그 작성이 쉽다는 장점이 있다. 



#### jsp정의와 구성요소

| 웹클라이언트                                                 | 웹 서버          |
| ------------------------------------------------------------ | ---------------- |
| html : 화면구성<br />css: 크기, 색상, 모양 <br />js jquery : 동작 (화면 변경) | servlet<br />jsp |



* servlet과 jsp 비교

  | servlet                                                      | jsp                                                          |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | 자바언어구현 + html태그 응답                                 | 자바언어구현 + html태그 응답                                 |
  | 자바 클래스 구조를 가짐<br />상속, 메소드, 오버라이딩이 정해져있음<br />(doGet/doPost/service)<br />자바문장 내부에 html태그 포함<br />(String 타입 저장) | html파일과 유사한 형식을 가짐<br />클래스, 상속, 메소드, 오버라이딩 구현X<br />내부적으로는 클래스,상속,오버라이딩 자동 변경<br />html파일 내부에 특정 태그 양식으로 자바 문장을 포함하는 형식<br /> |



* jsp 실행

  1. jsp 소스를 자바 소스로 변경한다 

     * html태그들은 out.write("")출력
     * 클래스 상속 jspService메소드 구현
     * <% %> 자바문장 실행

     해당 과정 및 메소드 구현은 workspace>.metadata>.plugins>org.eclipse.wst.server.core>temp0>work>Catalina>localhost>jsp>org>apache>jsp> .java 

     에서 확인 가능하다. 

  2. 컴파일한다
  3. 실행 결과 출력





#### 기본문법 (tag)

| 태그명   | 문법                                                         |
| -------- | ------------------------------------------------------------ |
| jsp태그  | <% 스크립트릿 태그 %><br /><%@ 지시자 page\|include%><br /><%! 선언문: 멤버변수나 메소드 선언 %><br /><%=출력, 속성값 표현 %><br /><%-- 주석 --%> |
| 액션태그 | <jsp:xxxx             />                                     |
| el표현식 | ${el언어}                                                    |
| JSTL     | <c:xxx     />                                                |

**주의**: <u>jsp속성값은 반드시 이중따옴표 " "</u>를 붙인다 



##### jsp 태그 



1.  page 지시자 태그 (directive tag)

* **<%@page %>** 

  * jsp가 자바소스를 변경하는 시점에서 tomcat에게 지시 사항 정의
    * 그렇기 때문에 반드시 처음에 기입해야 한다. 
    * "page"는 자바의 "this"키워드와 유사한 역할을 한다. (자기 자신 page를 가르킴)
    * contentType, import 등을 기입

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"
      import = "java.util.Date"
      %>
    <!--
  	자바소스 변경시에 tomcat에게 알려주는 내용들이 기입(응답하기 위해 반드시 필요한 부분)
  	page language, pageEncoding 생략 가능, contetType은 필수 
   	import가 필요할시 해당 태그에 기입--> 
  ```



* **<%@include %>**

  * 다른 jsp파일을 합쳐서 실행을 정의한다.

    * 예를 들어 3개 jsp파일에 공통 기능의 jsp파일이 필요하다면 공통 기능의 jsp파일을 생성하고 같이 사용이 가능하다.  

    아래과 같이 공통기능이 포함된 share.jsp파일이 있다면

    ````jsp
    <body>
    <% String name = "/test/imgs_company/main_img.png"; %>
    	<img src="<%=name%>" width="300" height="300">
    	<%=name%>
    </body>
    ````

    <%@include %>태그를 쓴다.

    ````jsp
    <%@ include file="share.jsp" %>
    ````

  * 하나의 jsp를 세 개의 jsp파일이 사용한다면, 이는 공유하는 하나의 파일을 생성하고 재사용하는 것이기 때문에 공통기능의 파일은 단 한 개만을 생성하면 된다. 



2. **<% 	%>**: 스트립트릿 태그

   * <% %> 태그 내부에 자바 문장을 그대로 사용하면 된다. 

   ````jsp
   <%
   	ArrayList<BoardDTO> list = (ArrayList)request.getAttribute("list");
   	int count = (Integer)request.getAttribute("count");
   	int pagecnt = count / 5;
   	%> 
   ````



3. **<%!      %>**: 선언문 태그

   * 멤버변수와 메소드를 추가할 때 사용한다. 

     * 해당 태그에 선언하는 변수는 스트립트릿 태그와 달리 멤버변수로 선언
     * 이 태그에는 오로지 선언만 가능

     ```jsp
     <%! String var = "첫번째";%>
     <%! 
       String var2 = "두번째";
     	System.out.println(var2); > 불가능, 선언만 가능 
     %>
     ```

   * <%   %>와 <%!   %>차이: 

     * <%   %> 내부에는 메소드 생성이 불가능하다. 이미 메소드 안에 생성되어 있는 태그이기 때문. (.metadata 내 파일 확인해보면 알 수 있음)  이 안에 생성되는 변수도 따라서 지역변수로 선언된다.



4. **<%=  %>**: 표현문 태그

   * 변수나 메소드의 결과값 등을 브라우저에 출력하는 용도

   * 내부에 속성을 넣는다. 

     ````jsp
     <%String name = "name"%>
     <%= name%>
     ````

     

   * 일종의 출력문이라고 생각하면 된다. out.println(); 과 같은 역할을 함. 



5. 주석

   * .jsp 에는 html태그와 자바 언어를 표현하기 위한 jsp태그가 함께 사용되기 때문에 사용에 주의해야 한다. 

   <!-- --> 

   : html 주석 - 브라우저 실행 제외

   <%--   --%>

   : jsp 주석 - jsp를 자바소스로 변경시 제외

   <% // %>

   : jsp를 자바소스로 변경시 포함, 자바 컴파일때 제외

   ````jsp
   <!--<%@ include%> --> : 주석처리 되지 않음
   <%--<%@ include%> --%> 
   ````

   



#### jsp 내장객체

jsp의 처리결과는 자바 변수 형태로 제공되고, 이렇게 처리하는 중에 자주 사용할만한 객체를 미리 만들어 제공한다. 미리 선언되어진 변수들, 이것을 내장객체라고 한다. 



* 내장객체 종류

| 종류        | 기능                                                         | servlet                                          |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------ |
| request     | 요청                                                         | doGet\|doPost\|service<br />HttpServletRequest   |
| response    | 응답                                                         | HttpServletResponse                              |
| out         | 응답<br /><%out.println("");%><br /><%=%>:표현문도 출력O     | PrintWriter out =<br />response.getWirter        |
| session     | jsp - 서블릿 데이터 공유                                     | HttpSession session = <br />request.getSession() |
| application | jsp - 서블릿 데이터 공유                                     |                                                  |
| config      | jsp - 서블릿 데이터 공유                                     |                                                  |
| exception   | <%@page<br />isErrorPage=true%> jsp파일만 내장객체 사용 가능 |                                                  |



예제 1) 

| SessionTestServlet        | session.jsp    |                               |
| ------------------------- | -------------- | ----------------------------- |
| id=jsp<br />->세션에 저장 | 세션 저장값 id | 브라우저 동작까지 session사용 |

````jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
	String session_id = " ";
	if(session.getAttribute("session_id") != null){
	session_id = (String)session.getAttribute("session_id");
	}else{//로그아웃을 했거나 서블릿이 실행하지 않았거나 
		out.println("로그아웃했거나 아직 로그인 전입니다.");
	}
	%>
	<h1><%=session_id %>회원님 로그인 하셨습니다. </h1>
	<h3><a href="sessiontest3.jsp">내 정보 보러 가기</a></h3>
	<h3><a href="sessiontest4.jsp">로그아웃 하러 가기</a></h3>
	<h3><a href="/jsp/sessiontest?id=jsp">다시 로그인 하러 가기</a></h3>
</body>
</html>
````

````jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<% 
String session_id = (String)session.getAttribute("session_id");
out.println("내 정보는 다음과 같습니다");
%>
</body>
</html>
````

````jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
	session.removeAttribute("session_id");
	%>
	<%="로그아웃되셨습니다." %>
</body>
</html>
````



* **예외처리(Exception)**

  * 예외처리는 예외처리를 할 전담 jsp파일을 생성하고, 그 파일로 모든 파일을 떠넘기는 형태를 만들 수 있다. 

    * 예외처리 떠넘김

    ````jsp
    <%@page errorPage="떠넘길 jsp파일 명" %>
    ````

    * 예외처리 받기

    ````jsp
    <%@page is ErrorPage=true %>
    <body>
    <%System.out.println(exception); %>
    </body>
    ````

    : true인 경우만 예외처리 ㅇ. false나 다른 값이 올 경우 예외처리를 받지 못 함. 

  예제)

  예외처리를 떠넘기는 파일(여러 파일이 동일 jsp에 예외를 떠넘길 수 있다)

  ````jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8" errorPage="b.jsp"%>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  	<%
  	String num = request.getParameter("num");//NumberFormatException
  	int num2 = Integer.parseInt(num);//NullpointerException
  	out.println("<h1>" + 0/num2 + "</h1>"); // ArithmeticException
  	%>
  </body>
  </html>
  ````

  예외처리를 받는 파일(예외처리만 전담으로 받는 파일)

  ````jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8" isErrorPage="true"%>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  	<%System.out.println(exception); %>
  	<%="서버에 임시적으로 문제가 발생하였습니다. 잠시 후 접속하세요." %>
  </body>
  </html>
  ````

  



#### 액션 태그

jsp파일은 html태그 + <% 자바문장 %>이 구분되고, 이러한 코드가 길어질 경우 복잡해질 가능성이 크다. 이 점에 있어서 더 간단하게 표현하기 위해, 자바 코드 대신 액션 태그들이 그 자리를 대신한다. 



**태그종류**

| 태그                     | 기능                                        |
| ------------------------ | ------------------------------------------- |
| <jsp:forward		/ >  | 서블릿 RequestDispatcher 클래스 포워드 기능 |
| <jsp:include         / > | 이미 있는 jsp를 현재 jsp에 포함             |
| <jsp:useBean       / >   | 객체를 생성하기 위한 new 연산자             |
| <jsp:setProperty    / >  | setter를 대신하는 태그                      |
| <jsp:getProperty    / >  | getter를 대신하는 태그                      |



* **<jsp:include         / >**

  *  <%@ include  %>가 정적이라면, 액션은 이미 공유된 파일 외에 각 공유받은 파일에서 파일 수정이 가능하다. 

    ````jsp
    <jsp:include page = "share.jsp">
    <jsp:param name = "img" value="b.png"/> :보낸 파라미터로 이미지가 바뀜. 
    </ jsp:include> 
    ````

    ````jsp
    <jsp:include page = "share.jsp" />
    :정적으로 사용할 경우
    ````

    * 동적으로 이미지가 변경되어지면서 include 된다. 

      | <jsp:include<br />액션=동적          | <%@include<br />디렉티브=정적         |
      | ------------------------------------ | ------------------------------------- |
      | 재사용<br />화면구성시 레이아웃 설계 | 재사용<br />화면 구성시 레이아웃 설계 |
      | 2개 jsp = > 2개의 자바소스           | 2개 jsp = 1개 자바소스                |
      | <jsp:param -  파라미터 전달 값>      | 변수 공유 가능 <br /><%String name%>  |

  * 수행 결과를 모두 합쳐서 출력한다. 

  * include 파라미터 전달 필요 없을 경우:  <jsp:include page = " " />

  * include 자바 객체 전달 경우

    ````jsp
    request.setAttribute("", 객체);
    <jsp:include page=" "  />
    ````

    

* **<jsp:forward		/ >**

  실행 과정

  <img src="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-12%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.16.12.png" alt="스크린샷 2021-04-12 오후 3.16.12" style="zoom: 50%;" />

  * 출력할 내용을 만드는 것은 b.jsp, 처리는 a.jsp

  ````jsp
  <jsp:forward page = " ">
  <jsp:param name = " " value = " " />
  </ jsp:forward>
  전달할 파라미터가 없는 경우: 
  <jsp:forward page = " "/>
  ````

  

* **<jsp:useBean       / >** , <jsp:setProperty    / >, <jsp:getProperty    / >

  * 웹 프로그램에서 여러 객체를 거치면서 만들어지는 데이터를 저장하거나 전달하는 데 사용. 

  * 일종의 DTO클래스, VO클래스와 같은 개념.

  * servlet , jsp 환경 + 어플리케이션 재사용이 가능한 자바 클래스

    아래는 객체 생성

  ````jsp
  <jsp:useBean id="클래스 변수이름" class="패키지명.클래스명"/> 
  (class import 안 되어있으면 import)
  ````

  * scope=*"   "*

  ````jsp
  <jsp:useBean id="dto" class="board.BoardDTO" scope="request"/>
  ````

  ​	위의 코드는 java로 따지면 아래와 같은 의미이다. 

  ````java
  if(request.getAttribute("dto") == null){
  	BoardDTO dto = new BoardDTO();
  	request.setAttribute("dto",dto); }
  	else{
  	dto = request.getAttribute("dto");
  	} 
  ````

  : 즉, form을 입력받고, (request을 통해) 객체가 만들어진 적이 없다면 생성하고 존재한다면 생성되어 있는 것을 사용하라는 의미를 가진 코드 

  * scope = " "에는 여러 값이 올 수 있다. ex. session, page.. 

  

  * DTO의 변수 이름은 html에서 값을 받아 올 name변수 이름과 같게 해주는 것이 좋다
    * jsp 액션태그에서는 htmlform에서 name 속성의 이름과 dto 변수 이름이 같다면, form에서 동일 이름의 값을 읽어오기 때문. 엄청난 편리성!
  * **<jsp:setProperty    / >**

  ````jsp
  <jsp:setProperty property="속성 이름" name ="자바 빈 이름" value="값"/>
  ````

  * * setter/getter 이름의 첫글자는 반드시 소문자

    * **속성 이름**: 본래 이름이 SetName인 메소드 이름은 > name으로 변경 

    * 속성 이름이 form으로 입력될 변수명과 같다면, 해당 변수 값이 액션태그가 가르키는 클래스의 set값으로 넘언간다. 즉, <u>value 생략 가능</u>

      * +) param

      ````jsp
      <jsp:setProperty property="title" name ="dto" param="title2" />
      :title 변수값이 없다면 title2의 파라미터를 넣겠다. jsp의 파라미터를 바꾸지 못하는 경우 사용
      ````

      

  * **<jsp:getProperty    / >**

  ````jsp
  <jsp:getProperty property="속성 이름" name="자바 빈 이름"/>
  ````









#### servlet과 jsp 연동

servlet과 jsp는 다음과 같은 경우에 각각 유용하다. 

* servlet: 요청과 처리를 하는 경우 (자바코드가 많음)
* jsp: 응답하는 경우 (html코드가 많음

이같은 특성에 따라 각 역할에 맞는 파일에 코드를 설계한 후, 연동시키는 것이 효율적이다.



게시판 예제: (DAO, DTO는 생략)

1)servlet

```java
package board;

import java.io.IOException;
import java.util.ArrayList;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/boardstart")
public class BoardServlet extends HttpServlet {
	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//   서블릿: 요청 - 처리 + jsp : 응답 
		String page = request.getParameter("page");
		int pageNum = 0;
		if(page == null) {
			pageNum = 1;
		}else {
			pageNum = Integer.parseInt(page);
		}
		BoardDAO dao = new BoardDAO();
		ArrayList<BoardDTO> list = dao.getBoardList(pageNum, 5);
		
		int count = dao.getBoardCount();
		request.setAttribute("count", count);
		request.setAttribute("list", list);
		RequestDispatcher rd = request.getRequestDispatcher("board/boardstart.jsp");
		rd.forward(request, response);
	}

}
```

: servlet에서는 요청 받고 처리할 코드만 기입, 그리고 실행 할 jsp로 forward 



jsp

```jsp
<%@page import="java.util.ArrayList, board.BoardDTO"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<style type="text/css">
table, td{border:2px solid pink;}
table{margin: auto;}
</style>
</head>
<body>
	<%
	ArrayList<BoardDTO> list = (ArrayList)request.getAttribute("list");
	int count = (Integer)request.getAttribute("count");
	int pagecnt = count / 5;
	%> 
	
	<table>
	<%
	for(int i = 0; i < list.size(); i++) {
	%>
	<tr>
	<td><%=list.get(i).getSeq()%></td>
	<td><%=list.get(i).getTitle()%></td>
	<td><%=list.get(i).getWriter()%></td>
	<td><%=list.get(i).getViewcount()%></td>
	</tr>
	<%
	}
	%>
	<% if(count % 5 != 0) { pagecnt = pagecnt+1; }
	for(int i = 1; i <= pagecnt ; i++) { 
	out.println("<a href = 'boardstart?page=" + i + "'>" + i + "</a>");	
	} %>
	</table>
</body>
</html>
```

