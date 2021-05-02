### Servelt의 DB 연동



* client와 server 통신

| client                                                       | server                                                      |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| http://ip:port/컨텍스트명/a?id=jdbc                          | a -> AServlet -> doGet(){<br />request.getParameter("id")}; |
| http://ip:port/컨텍스트명/b?id=jdbc<br />서버 종료 시점까지 현재 컨텍스트의 모든 서블릿끼리 공유 O | b -> BServlet -> doGet(){<br />request.getParameter("id")}; |



자바에서 DB를 연결해 DAO, DTO로 데이터를 전송시키고 받아왔다면, 이 과정을 servlet을 통해 서버와 연결해본다.

* jdbc api 이용
* 요청-처리(DB연동 필요시 jdbc) - 응답
* 서블릿코드와 처리 코드는 클래스별로 분리해서 작성한다. 
  * CRUD : create(저장) read(조회) update(수정) delete(삭제) 기능 

(예제 추가)







# Servlet 확장 API

| 서블릿 기본 api     | 확장 api - 서블릿 연동                  |
| ------------------- | --------------------------------------- |
| HttpServlet         | RequestDistpatcher                      |
| HttpServletRequest  | ServletContext                          |
| HttpServletResponse | ServletConfig<br />(tomcat-servlet연동) |

### 서블릿 연동하기

 : 하나의 서블릿에서 다른 서블릿이나 JSP와 연동하는 방법



#### ConnectionPool

*  ConnectionPooling  : 미리 일정 개수의 커넥션을 생성해놓고 전달하는 방식 
  * 자바에서 DB에 직접 연결해 처리하는 JDBC의 경우, 드라이버를 로드하고 connection 객체를 받아와야 한다. 매번 사용자가 요청할 때마다 드라이버를 로드하고 커넥션 객체를 생성, 연결, 종료를 해야 한다는 의미. 비효율적. 
  * 커넥션 풀은 웹 컨테이너가 실행되면서 DB와 미리 connection을 해놓은 객체들을 pool에 저장해두었다가 클라이언트 요청이 오면 connection을 빌려주고, 처리가 끝나면 다시 connection을 반납받아 pool에 저장하는 방식



<img src="cp-s1.png" alt="cp-s1" style="zoom:48%;" />

* 특징

  * 웹 컨테이너가 실행되면서 connection 객체를 미리 pool에 생성
  * http 요청에 따라 pool에서 connection 객체를 사용 후 반환
  * connection 부하를 줄이고 연결 관리가 가능, pool에 이미 connection이 생성되어 있기 때문에 연결시간 단축
  * connection 재사용 덕분에 생성되는 커넥션 수 제한 가능

  

* ConnectionPooling 기능을 갖고있는 api가 Datasource

  * 직접 구현의 방법 혹은 서버가 미리 구현해서 제공

  * tomcat server.xml 파일을 설정

    ````html
    <Context docBase="servlettest" path="/servlettest" reloadable="true" source="org.eclipse.jst.jee.server:servlettest">
         		
         		<Resource 
    	      name="jdbc/myoracle" 
    	      MaxActive="5" 
    	      auth="Container" 
    	      maxIdle="5" 
    	      maxWait="-1" 
    	      type="javax.sql.DataSource" 
    	      
    	      driverClassName="oracle.jdbc.driver.OracleDriver" 
    	      password="jdbc" 
    	      url="jdbc:oracle:thin:@127.0.0.1:1521:xe" 
    	      username="jdbc"/>
         		
          </Context>
    ````

    



#### 서블릿 연동 역할

| RequestDispatcher  | 요청 - 처리 - 응답(A+B)될때까지만 연동<br />요청 처리가 되는 동안만 공유된다. (요청공유)<br />request.setAttribute("name", 객체)<br />request.getAttribute("name")<br />request.removeAttribute("name") |
| ------------------ | ------------------------------------------------------------ |
| **ServletContext** | context = web application <br />=dynamic web project(html, java,jsp)<br /><br />컨텍스트 공유: **동일한 dynamic web project안에 존재하는 서블릿끼리 공유.** <br />context.setAttribute("name", Object)<br />context.getAttribut("name")<br />context.remove.Attribut("name")<br />tomcat이 공유중단되지 않는 이상 계속 공유됨. |
| **HttpSession**    | 세션공유<br />session.getAttribute("name", Object)<br />session.setAttribut("name")<br />sesstion.remove.Attribute("name") |
| **Servletconfig**  | tomcat web.xml - 서블릿 연동<br />tomcat @WebServlet<br />**현재서블릿만 사용 가능** |

* 서블릿끼리 결합되어 연동 가능한 범위

  * forward: 요청해서 공유하는 서블릿까지,  즉  포워드하는 파일까지만

  * context: 동일한(현재) 다이나믹 웹 프로잭트 에 있으면 공유 가능. 브라우저가 닫혔다가 열려도 공유될 정보가 남아있음.

  * Session: 브라우저를 열고 동일 브라우저에서 실행하는 서블렛들끼리. 브라우저가 닫혔다가 열리면 공유될 정보가 사라져있음.

    | 시기                         | API                                                          |
    | ---------------------------- | ------------------------------------------------------------ |
    | 요청-응답 종료               | HttpServletRequest<br />setAttribute("", 객체)<br />getAttribute("")<br />removeAttribute("") |
    | 브라우저 종료                | HttpSession<br />setAttribute("", 객체)<br />getAttribute("")<br />removeAttribute("") |
    | 톰캣서버 종료 (가장 큰 범위) | ServletContext<br />setAttribute("", 객체)<br />getAttribute("")<br />removeAttribute("") |

    

* 공유가능한 데이터 객체 방법: 

  * setAttribute(" ", object) : 객체 set
  * getAttribute(" ") : 객체 get
  * removeAttribute(" ") : 객체 remove



### 1. forward

#### forward 기능

* 요청에 대한 추가 작업을 다른 서블릿에게 수행하도록 한다.
* 요청(request)에 포함된 저보를 다른 서블릿이나 JSP와 공유할 수 있다.
* 요청에 정보를 포함시켜 다른 서블릿에 전달할 수 있다.
* 모델2 개발 시 서블릿에서 JSP로 데이터를 전달하는 데 사용된다. 



포워드 방법은 총 네가지로 제시되는데, dispatch를 추천한다고 한다.

#### forward 방법, dispatch

* 서블릿이 직접 요청하는 방법

* RequestDispatcher 클래스의 forward() 메소드 이용

  RequestDispatcher dis = request.getRequestDispatcher("포워드할 서블릿 혹은 JSP");

  dis.forward(request, response);

  *  request와 response 모두 전달하는 것, 일종의 위임
  
  ````java
  @WebServlet("/forward1")
  public class Forward1Servlet extends HttpServlet {
  
  	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  		String id = request.getParameter("id");
  		//get/setparameter-String (객체전달 x) 전송되면 무조건 스트링. 
  		//get/setAttribute - String + 객체 전달 ㅇ 서블릿끼리니까 객체를 줄 수 있어야 함(자바언어)
  		//현재 서블릿이 forward2로 서블릿 객체를 전달 
  		BoardDTO dto = new BoardDTO();
  		dto.setTitle("제목");
  		dto.setContents("내용");
      
  		request.setAttribute("board", dto );
      //이름과 객체를 같이 줌. 이 상태의 리퀘스트가 그대로 전달. board에 있는 dto를 전달? 
  		
  		RequestDispatcher dis = request.getRequestDispatcher("forward2"); //forward2랑 공유하겠다. 
  		dis.forward(request, response); 
  		//forward시에는 이전 응답하겠다고 출력에 저장해놨던 것이 삭제되고 새로운 forward로 이동 
  		//따라서 앞 문장 필요 없음. 
  		//파라미터 공유가 됨. 그러나 최종적으로는 두번째페이지에서만 출력. 첫번째 페이지는 출력 없음( 삭제 )
  	}
  
  ````

}
  ````
  
  ````java
  @WebServlet("/forward2")
  public class Forward2Servlet extends HttpServlet {
  
  	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  		String id = request.getParameter("id");
  		response.setContentType("text/html;charset=utf-8");
  		response.getWriter().println("<h1>(forward2)로그인아이디=" + id + "</h1");
  		
  		BoardDTO dto = (BoardDTO)request.getAttribute("board"); //원래는 Object타입, 형변환
  		response.getWriter().println("<h1>" + dto.getTitle() + ":" + dto.getContents() + "</h1>");
  		
  	}
  
}
  ````






#### 특징

* url을 통해서만 호출 가능, get post 정해진 방식으로 요청, b 타입의 객체를 만들지 못한다.
* 대신 dispatcher 사용. 그리고 변수에 요청해서 연동할 url을 적는다. 
* forward는 연동을 하는데 처음에 a를 요청, 요청 후 b가 요청, b가 행하고 그것을 되돌려주는 형태. 
* b.forward(request, response); > a에서 받은 request와 response 모두 전달하는 것, 일종의 위임
* request.getParameter(" "); 파라미터값은 같이 공유 가능, ( String 값만 가능하기 때문)
* request.setAttribute("n", Object); 받은 쪽에서는, (b)   request.getAttribute("n", Object); : 대신 형변환이 필요, <u>기본적으로 Object 타입</u>이기 때문에. 



### 2. Context





### 3. Session





### 4. config



