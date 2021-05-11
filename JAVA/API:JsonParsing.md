

### 인공지능 api 사용하기 

> naver clova 인공지능 api를 사용
>
> * 인증 키를 발급받고, 코드에서 호출 구현이 가능
>   * 인증 키(id, secret)는 코드에 작성



##### 작동방식

파이썬 

> 다음 코드는 네이버에서 예시로 제공하는 코드 

````python
import os
import sys
import requests
client_id = "YOUR_CLIENT_ID"
client_secret = "YOUR_CLIENT_SECRET"
url = "https://naveropenapi.apigw.ntruss.com/vision/v1/celebrity" // 유명인 얼굴인식
files = {'image': open('YOUR_FILE_NAME', 'rb')}
headers = {'X-NCP-APIGW-API-KEY-ID': client_id, 'X-NCP-APIGW-API-KEY': client_secret }
response = requests.post(url,  files=files, headers=headers)
rescode = response.status_code
if(rescode==200):
    print (response.text)
else:
    print("Error Code:" + rescode)

````



자바

> 다음 코드는 네이버에서 예시로 제공하는 코드

````java
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLConnection;

// 네이버 얼굴인식 API 예제
public class APIExamFace {

    public static void main(String[] args) {

        StringBuffer reqStr = new StringBuffer();
        String clientId = "YOUR_CLIENT_ID";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "YOUR_CLIENT_SECRET";//애플리케이션 클라이언트 시크릿값";

        try {
            String paramName = "image"; // 파라미터명은 image로 지정
            String imgFile = "이미지 파일 경로 ";
            File uploadFile = new File(imgFile);
            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision/v1/celebrity"; // 유명인 얼굴 인식
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setUseCaches(false);
            con.setDoOutput(true);
            con.setDoInput(true);
            // multipart request
            String boundary = "---" + System.currentTimeMillis() + "---";
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
            con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
            OutputStream outputStream = con.getOutputStream();
            PrintWriter writer = new PrintWriter(new OutputStreamWriter(outputStream, "UTF-8"), true);
            String LINE_FEED = "\r\n";
            // file 추가
            String fileName = uploadFile.getName();
            writer.append("--" + boundary).append(LINE_FEED);
            writer.append("Content-Disposition: form-data; name=\"" + paramName + "\"; filename=\"" + fileName + "\"").append(LINE_FEED);
            writer.append("Content-Type: "  + URLConnection.guessContentTypeFromName(fileName)).append(LINE_FEED);
            writer.append(LINE_FEED);
            writer.flush();
            FileInputStream inputStream = new FileInputStream(uploadFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            writer.append(LINE_FEED).flush();
            writer.append("--" + boundary + "--").append(LINE_FEED);
            writer.close();
            BufferedReader br = null;
            int responseCode = con.getResponseCode();
            if(responseCode==200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            } else {  // 오류 발생
                System.out.println("error!!!!!!! responseCode= " + responseCode);
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}

````



* 전송할 url을 알려주고 전송 방식이 GET인지 POST인지 선언. 

* html header: 서버에서 요구하는 추가정보를 요구.

  * 실제 데이터가 존재, 그리고 데이터를 표현해줄 수 있는 클라이언트아이디랑, 시크릿

    서버에 연결해서 파일을 읽고 처리하는데 클라이언트 아이디, 시크릿이 필요 > 이것을 처리하는 부분

    JAVA

    ````java
     con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
                con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
                con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
    ````

    PYTHON

    ```python
    headers = {'X-NCP-APIGW-API-KEY-ID': client_id, 'X-NCP-APIGW-API-KEY': client_secret }
    ```

* 그 뒤에 데이터, 파일을 읽는다 

  * 파일 처리에 필요한 코드

    JAVA

    ```java
    PrintWriter writer = new PrintWriter(new OutputStreamWriter(outputStream, "UTF-8"), true);
                String LINE_FEED = "\r\n";
                // file 추가
                String fileName = uploadFile.getName();
                writer.append("--" + boundary).append(LINE_FEED);
                writer.append("Content-Disposition: form-data; name=\"" + paramName + "\"; filename=\"" + fileName + "\"").append(LINE_FEED);
                writer.append("Content-Type: "  + URLConnection.guessContentTypeFromName(fileName)).append(LINE_FEED);
                writer.append(LINE_FEED);
                writer.flush();
    ```

    PYTHON

    ```python
    response = requests.post(url,  files=files, headers=headers)
    rescode = response.status_code
    ```





#### SPRING MVC에서 API 가져오기

> MVC에서는 기능에 따라 Controller, Service, DAO, VO 클래스로 구별한다. 
>
> API소스의 경우 데이터를 해당 서비스제공사 측에서 요청을 받고 응답해주기 때문에, 따로 DB연결할 필요 없으므로 기능상 Service에 구현한다. 



Service Interface

> Interface는 반드시 구현해야 할 매소드를 기입해주는 곳. 객체지향의 특성상 확장은 유용하게, 수정은 닫혀있는 방식으로 구현 

```java
package naver.cloud;

public interface NaverService {
	public String test(String image);
	
}
```



Service 

```java
package naver.cloud;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLConnection;

import org.springframework.stereotype.Service;

@Service
public class NaverFaceService implements NaverService {

	@Override
	public String test(String image) {
        StringBuffer response = new StringBuffer();
        StringBuffer reqStr = new StringBuffer();
        String clientId = "clientId";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "clientSecret";//애플리케이션 클라이언트 시크릿값";

        try { //<form action="url" method=post endtype="multipart/form-data   < input type=file name="image"
        	
            String paramName = "image"; // 파라미터명은 image로 지정. (얼굴 인식 url 요구 파라미터 이름)
            String imgFile = "File path" +image;
            //Controller에서 image매개변수를 받고, image이름 값 앞에 path를 기입
            File uploadFile = new File(imgFile);
            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision/v1/celebrity"; //얼굴 인식
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setUseCaches(false);
            con.setDoOutput(true);
            con.setDoInput(true);//  서버 전송 데이터 추가 있다
            // multipart request
            String boundary = "---" + System.currentTimeMillis() + "---";
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
            con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
            OutputStream outputStream = con.getOutputStream();
            PrintWriter writer = new PrintWriter(new OutputStreamWriter(outputStream, "UTF-8"), true);
            String LINE_FEED = "\r\n";
            // file 추가
            String fileName = uploadFile.getName();
            System.out.println("'" + fileName + "'");
            writer.append("--" + boundary).append(LINE_FEED);
            writer.append("Content-Disposition: form-data; name=\"" + paramName + "\"; filename=\"" + fileName + "\"").append(LINE_FEED);
            writer.append("Content-Type: "  + URLConnection.guessContentTypeFromName(fileName)).append(LINE_FEED);
            writer.append(LINE_FEED);
            writer.flush();
            FileInputStream inputStream = new FileInputStream(uploadFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            writer.append(LINE_FEED).flush();
            writer.append("--" + boundary + "--").append(LINE_FEED);
            writer.close();
            //===================id,  시크릿키, 이미지파일 읽어서 요청 보내기 
        
            //응답 받기
            BufferedReader br = null;
            int responseCode = con.getResponseCode();
            if(responseCode==200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));// {}
            } else {  // 오류 발생 400, 500
            	System.out.println(con.getResponseMessage());
                System.out.println("error!!!!!!! responseCode= " + responseCode);//400
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                //StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
            return e.toString();//클라이언트 파일...오류메시지
          
        }
        return response.toString();// 서버로부터의 결과(오류,정상결과)
	}

}
```



Controller

```java
package naver.cloud;

import java.io.File;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class NaverController {
	@Autowired
	NaverFaceService service;
	
	@RequestMapping("/faceinput")
	public ModelAndView faceinput() {
		ModelAndView mv = new ModelAndView();
		File f = new File("/Users/lulala/images/");
		String[] filelist = f.list(); //여러 파일이 들어있는 폴더를 path로 지정할 경우, list()함수 사용이 가능
		mv.addObject("filelist", filelist);//view에서 파일명 list를 받을 것
		mv.setViewName("/naver/faceinput")
		return mv;
	}
	@RequestMapping(value="/face", method=RequestMethod.GET)
	public ModelAndView face(String image) {
		String result = service.test(image);
		ModelAndView mv = new ModelAndView();
		mv.addObject("faceResult", result);
		mv.setViewName("/naver/face");
		return mv;
	}
	
}
```



FaceInput jsp

> 응답할 결과를 요청하는 view(파일 전송)

````jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script src = "jquery-3.2.1.min.js"></script>
<script>
$(document).ready(function(){
  });
</script>
</head>
<body>
  <!--Controller에서 받은 filelist데이터로 파일 명 추출, 링크 생성// /face는 get방식으로 데이터 받음-->
<%
String[] filelist = (String[])request.getAttribute("filelist");
for(String file : filelist){
	%>
	<a href="/face?image=<%=file%>"> <%=file%> <img src="/images/<%=file%>" width=100px> </a><br>
<%
}
%>
</body>
</html>
````



Face.jsp

> 결과값을 보여주는 view

````jsp

<%@page import="java.math.BigDecimal"%>
<%@page import="org.json.JSONArray"%>
<%@page import="org.json.JSONObject"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>    
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script src="jquery-3.2.1.min.js"></script>
<script>
$(document).ready(function() {

});
</script>
</head>
<body>
<h1> 닮은 연예인 찾아주기 </h1>

<%
// 자바 String 을 json 변환  파싱
String faceResult = (String)request.getAttribute("faceResult");
JSONObject obj = new JSONObject(faceResult);
Object imsi = obj.get("faces");//faces : [celebrity : {value:.. confidence : }, {}]
JSONArray faces = (JSONArray)imsi;
boolean find = false;
for(Object cele : faces){
	JSONObject celebrity = (JSONObject) ((JSONObject)cele).get("celebrity");
	find = true;
	//String value = (String)celebrity.get("value");
	BigDecimal confidence = (BigDecimal)celebrity.get("confidence");
	// confidence
	out.println("닮은 연예인이름=" + celebrity.get("value") + " , 닮은 확률=" 
	+ Math.round(confidence.doubleValue() * 100) + "%<br>");

}

String image = request.getParameter("image");
if( find == false ){
	out.println("닮은 연예인을 찾을 수가 없습니다.<br>");
}

%>


<img src="/images/<%=image %>" >
</body>
</html>

````

* Json Pasing을 JSONObject 라이브러리로 처리 







#### JSON Parsing

> 외부 API를 사용할 경우, 결과 return값이 JSON 코드인 경우가 있다. 이 경우 {"변수명": {"a":"문자값", "b":1213}식의 키워드:데이터 값을 return되는데, 여기서 필요한 키워드의 값을 가져올 수 있어야 한다. 

* JSONObject 라이브러리를 사용하지 않는 경우

  {"info":{"size":{"width":264,"height":200},"faceCount":1},"faces":[{"celebrity":{"value":"송혜교","confidence":0.654766}}]}

  위와 같이 값이 return되기 때문에, 각 문자열을 쪼개주어 해당 키워드의 값을 알아내야 한다. 

  아래는 라이브러리를 사용하지 않고 자바 코드로 value값과 confidence값을 추출한 코드이다. 

````jsp
<%
String faceResult = (String)request.getAttribute("faceResult");
out.println(faceResult+"<br>");
String faceInfo[] = faceResult.split("\"faces\":");
out.println(faceInfo[1] +"<br>");
String celeInfo[] = faceInfo[1].split("\"celebrity\":");
out.println(celeInfo[celeInfo.length - 1] + "<br>") ;
String one = celeInfo[celeInfo.length - 1] ;
int valueIndex = one.indexOf("\"value\":");
int valueLength = "\"value\":".length();
int confiIndex =  one.indexOf("\"confidence\":");
int confiLength = "\"confidence\":".length();

out.println(celeInfo[celeInfo.length - 1].substring(valueIndex + valueLength,  confiIndex-1) + "<br>");
out.println(celeInfo[celeInfo.length - 1].substring(confiIndex + confiLength,  confiIndex + confiLength + 8) + "<br>");
%>
````





### JSONObject



##### JSON 형식

JSON은 "key-value"가 쌍으로 이루어진 데이터 집합으로 이루어져 있다. 만약 같은 그룹에 여러 데이터가 존재하면, 공통 그룹 데이터를 하나로 묶는 것이 { }로 가능하다.

````
student{
"name" : "david",
"age"  : 20
"gender" : "male"
}
````

한 객체의 여러 정보를 하나로 묶을 때는 중괄호 { }를 사용한다. 

: 그리고 이러한 구조로 되어 있는 것은 <u>JSONObject 타입</u>이다. 



배열 타입의 경우를 생각해본다. 만약 저런 공통 그룹 데이터 { }가 여러개라면? 

````
"Student" : [{
"name" : "David",
"age"  : 20
"gender" : "male"
}, {
"name" : "Nicole",
"age"  : 21
"gender" : "female"
}, {
"name" : "Dzama",
"age"  : 19
"gender" : "male"
}
]
````

Student라는 key 값에 여러 object의 value를 가진다. 

: 이러한 구조는 <u>JSONArray 타입</u>이다.



* JSONObject
  * key:value 쌍을 중괄호{ }로 담고 있는 객체 구조
  * key value 구분은 :
  * 그룹당 구분은 ,
* JSONArray
  * 배열 구조 
  * 대괄호 안에 값을 담고, comma(,)로 값을 분류
  * index 사용 가능 (순서가 있다)





* **JSONObject Library**

  * 해당 라이브러리를 다운받으면 과정이 훨씬 간결해진다. 

  * pom.xml에 라이브러리 다운

    ````html
    <!-- for jason -->
    		<dependency>
    		<groupId>org.json</groupId>
    		<artifactId>json</artifactId>
    		<version>20201115</version>
    		</dependency>
    ````







  아래는 라이브러리 사용해서 값 추출하기 

  ````json
  <%
  // 자바 String 을 json 변환  파싱
  String faceResult = (String)request.getAttribute("faceResult");
  JSONObject obj = new JSONObject(faceResult);
  Object imsi = obj.get("faces");//faces : [celebrity : {value:.. confidence : }, {}]
  JSONArray faces = (JSONArray)imsi;
  boolean find = false;
  for(Object cele : faces){
  	JSONObject celebrity = (JSONObject) ((JSONObject)cele).get("celebrity");
  	find = true;
  	//String value = (String)celebrity.get("value");
  	BigDecimal confidence = (BigDecimal)celebrity.get("confidence");
  	// confidence
  	out.println("닮은 연예인이름=" + celebrity.get("value") + " , 닮은 확률=" 
  	+ Math.round(confidence.doubleValue() * 100) + "%<br>");
  }
  
  String image = request.getParameter("image");
  if( find == false ){
  	out.println("닮은 연예인을 찾을 수가 없습니다.<br>");
  }
  %>
  ````

  

