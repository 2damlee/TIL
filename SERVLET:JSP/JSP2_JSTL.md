#### EL표현식/ JSTL

> jsp의 목적은 짧고, 간결하게 자바의 긴 문장식을 없애는 것 

| el표현식 | ${el언어}       |
| -------- | --------------- |
| **jstl** | **<c:xxx   />** |

* JSTL: Jsp Tag Libarary

* EL: Expression Language

  * jsp 파일 내부에서 사용
  * jstl과 el은 다른 언어

  

  ##### el표현식

  ​			**${        }**

  * 기본 연산자와 특징

    * el은 부호 외에 다른 연산자 키워드도 제공
    * /div    %mod    ==eq    != ne    < lt    >ge    &&and    ||or    !not   
    * empty: 값이 null이면 true 반환

    ````jsp
    h1>${null}<!-- null은 무시(오류나지 않음) -->
    덧셈: ${10 + 20 }
    덧셈: ${'10' + 20 }<!-- 자동 형변환 -->
    덧셈: ${'el' += 20 }<!-- 문자열 결합은 +=, +는 형변환 오류 -->
    덧셈: ${null + 20 }</h1><!-- null은 0으로 변경 -->
    나눗셈: ${20/10}</h1>
    나눗셈: ${20 div 10}</h1>
    나머지: ${20%10}</h1>
    나머지: ${20 mod 10}</h1>
    비교: ${20 > 10}</h1>
    비교: ${20 gt 10}</h1>
    비교: ${20 lt 10}</h1>
    비교: ${20 eq 10}</h1>
    비교: ${20 ne 10}</h1>
    조건연산: ${20 != 10? "같지않다":"같다"}</h1>
    ${empty i}</h1><!-- i가 null값인지 i == null -->
    ````

  

  ##### 표현언어 내장객체

  | 내장객체         | 기능                                                      |
  | ---------------- | --------------------------------------------------------- |
  | pageScope        | page영역에 바인딩 된 객체 참조                            |
  | requestScope     | reqeust에 바인딩 된 객체 참조                             |
  | sessionScope     | session에 바인딩 된 객체 참조                             |
  | applicationScope | applicaiton에 바인딩 된 객체 참조                         |
  | param            | 한 개 값의 요청 매개변수<br />request.getParameter()      |
  | paramValues      | 여러 값의 요청 매개변수<br />request.getParameterValues() |
  | Cookies          | 쿠키 이름 값 반환                                         |
  | pageContext      | pageContext객체 참조                                      |
  | initParam        | 초기화 매개변수 이름 값 반환                              |

  

  **Scope**

  | jsp                                                          | el                                                           |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | request.setAttribute("name", 객체)<br />(Type)request.getAttribute("name")<br />이동, 포함되는 파일까지 공유 | ${requestScope.name}<br />형변환 필요 없음, name 그대로 사용하면 됨 |
  | session.setAttribute("name", 객체)<br />(Type)session.getAttribute("name")<br />브라우저 실행시까지 모든 파일 공유 | ${sessionScope.name}                                         |
  | application.setAttribute("name", 객체)<br />(Type)application.getAttribute("name")<br />tomcat서버의 같은 웹프로젝트의 모든 파일<br />(Servlet Context 이름 ) | ${applicationScope.name}                                     |

  ````jsp
  jsp의 경우:
  <jsp:getProperty property="title" name="dto"/><br>
  ````

  ````jsp
  ${dto.title}
  <!-- bean의 이름을 그대로 사용, get메소드는 get 삭제, 첫글자 소문자 -->
  ${requestScope.message} 
  <!-- request 안에 Attribute로 전달햇을 경우, requestScope
  parameter로 전달 한 경우는 param.name -->
  ````

  ```jsp
  ${paramValues.location[0]}
  <!--paramValues는 배열로 리턴, 해당 값을 지정해야 함
  ```

  * 만약 동일한 변수로 Scope.name을 지정한 경우 우선순위는 아래와 같다.

    pageScope > request > session > application

  

  

  #### JSTL

  JSTL을 사용하려면 jstl core 라이브러리 설치가 필요하다. 

  > ojdbc6.jar - > main javar - > jre system library에 해당 라이브러리를 넣어준다. (현재 다이나믹 웹 프로젝트만 사용 가능)

  설치 후, c태그가 등장하기 전에(가급적이면 초입부에) 다음과 같이 기입해준다.

  ````jsp
  <%@ taglib prefix="c" uri ="http://java.sun.com/jsp/jstl/core" %>
  ````

  



**태그와 기능**

| 태그           | 기능                         |
| -------------- | ---------------------------- |
| < c:set>       | 변수 지정                    |
| < c:remove>    | 변수 제거                    |
| < c:if>        | 조건문                       |
| < c:choose>    | switch문                     |
| < c:forEache>  | 반복문                       |
| < c:forTokens> | 토큰 처리 사용               |
| < c:import>    | url을 이용해 jsp에 자원 추가 |
| < c:redirect>  | response.sendRedirect()      |
| < c:url>       | 요청 매개변수로부터 url생성  |

| < c:out>   | JspWriter에 내용 처리 후 출력 |
| ---------- | ----------------------------- |
| <c:catch > | 예외처리                      |



* 변수선언에 관련된 태그 **<c:xxxx  />**

  * <c:set var = " " value = "<%=자바변수%>" /> : 변수 선언

  ````jsp
  <% String a = "jsp"; %>
  <c:set var="name" value="<%=a%>" 
  ````

  * <c:out value=" "/> : 출력

  ````jsp
  <c:out value="<%=a %>"/>
  ````

  * <c:remove var =" "/> : 변수 삭제

  ````jsp
  <c:remove var = "name" />
  ````

  

* **조건문**에 관련된 태그 

  * **<c:if test =  />**
    * 조건이 분할될 때

  ````jsp
  <c:if test = "조건">
  조건 만족시 수행 내용 정의
  </c:if>
  <c:if test = "${1<=0}">
  조건 만족시 수행 내용 정의
  </c:if>
  ````

  * **<c:choose />**
    * 다중조건문의 경우

  ````jsp
  <c:choose>
  	<c:when test="${조건}">
    조건을 만족 시 수행 내용 정의
    </c:when>
  </c:choose>
  ````

  예제)

  ````jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <%@ taglib prefix="c" uri ="http://java.sun.com/jsp/jstl/core" %>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  <c:if test = "${ empty param.id }">
  	<h1>id 입력은 필수입니다.</h1>
  </c:if>
  <c:if test = "${ !empty param.id }">
  	<h1>${param.id} 회원님 입장하셨습니다.</h1> 	
  		<c:choose>
  			<c:when test="${param.age <= 13}">
  				<h3 style = color:green>초등학생입니다</h3>
  			</c:when>
  			<c:when test="${param.age <= 16}">
  				<h3 style = color:blue>중학생입니다</h3>
  			</c:when>
  			<c:when test="${param.age <= 19}">
  				<h3 style = color:gray>고등학생입니다</h3>
  			</c:when>
  			<c:otherwise>
  				<h3 style = color:orange>성인 인증 되었습니다</h3>
  			</c:otherwise>
  	 	</c:choose>
  	</c:if>
  
  </body>
  </html>
  ````

  



* **반복문**

  * **<c:forEach   />**

  ````jsp
  <c:forEach begin="1" step="1" end="10">
   	수행내용
  </c:forEach>
  :1부터 시작해서 1씩 증가해서 10번 반복 
  
  <c:forEach items ="배열리스트 맵" var = "i">
   	${i}
  </c:forEach>
  : collection 형태에 쓸 수 있는 반복문. 반복되는 동안 데이터들을 i로 지어주겠다, 리스트나 맵에 있는 데이터가 존재하지 않을때까지 하나씩 출력될 것. 
  ````

  반복문 예제모음)

  ````jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8" %>
  <%@ page import = "java.util.ArrayList" %>
  <%@ page import = "board.BoardDAO" %>
  <%@ page import = "board.BoardDTO" %>
  <%@ page import="java.util.HashMap"%>
  <%@ taglib prefix="c" uri ="http://java.sun.com/jsp/jstl/core" %>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  	<!-- 1-10 정수 총합 -->
  	<h1>1-10 정수 총합</h1>
  	<% int sum = 0; %>
  	<c:set var="sum" value="<%=sum %>"/>
  	<c:forEach begin="1" end="10" step="1" var="index">
  	
  	${index}까지의 총합 = ${sum = sum + index}<br>
  	</c:forEach>	
  
  	<% String[] colors = {"빨강", "노랑", "파랑", "보라", "검정", "흰색"};
  	pageContext.setAttribute("el_colors", colors);
  	%>
  	
  	<c:forEach items="<%=colors %>" var="col">
  	${col }<br>
  	</c:forEach>
  	
  	<c:forEach items="${el_colors}" var="col">
  	${col}<br>
  	</c:forEach>
  	
  	<% BoardDAO dao = new BoardDAO();
  	   ArrayList<BoardDTO> list = dao.getBoardList();
  	   pageContext.setAttribute("boardlist", list);
  	%>
  	<!-- ${board.title} -- public board.gettitle() 호출 출력 -->
  	<c:forEach items="${boardlist}" var="board" >
  	${board.title}:${board.contents}:${board.writer}:${board.viewcount}<br>
  	</c:forEach>
  	<!-- list: index 관리, 저장 순서 조회 가능
  		 map: index가 없음, 데이터의 형식이 (key, value)로 구성되어 있음. -->
  	<%
  	HashMap<String, String> map = new HashMap<String, String>(); 
    //키도, 값도 String 타입
  	map.put("red", "빨강");
  	map.put("blue", "파랑");
  	map.put("green", "녹색");
  	map.put("white", "흰색");
  	map.put("black", "검정");
  	pageContext.setAttribute("colorsMap", map);
  	%>
  	<c:forEach items="${colorsMap}" var = "col" varStatus="st">
  	조회된 ${st.count} 번째 데이터: ${col.key} - ${col.value}<br>
  	</c:forEach>
  	
  	<c:forEach items="${colorsMap}" var = "col" varStatus="st">
  		<c:if test = "${st.first}">
  		 - ${st.current.key} - ${st.current.value}<br>
  		 </c:if>
  	</c:forEach>
  	
  	
  </body>
  </html>
  ````

  