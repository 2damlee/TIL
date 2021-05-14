# JSON Parsing

- JSONObject 라이브러리를 사용하지 않는 경우

    key:value 값이 return되기 때문에, 각 문자열을 쪼개주어 해당 키워드의 값을 알아내야 한다

### **JSON 형식**

JSON은 "key-value"가 쌍으로 이루어진 데이터 집합으로 이루어져 있다. 만약 같은 그룹에 여러 데이터가 존재하면, 공통 그룹 데이터를 하나로 묶는 것이 { }로 가능하다.

```
student{
"name" : "david",
"age"  : 20
"gender" : "male"
}
```

한 객체의 여러 정보를 하나로 묶을 때는 중괄호 { }를 사용한다.

: 그리고 이러한 구조로 되어 있는 것은 JSONObject 타입이다.

배열 타입의 경우를 생각해본다. 만약 저런 공통 그룹 데이터 { }가 여러개라면?

```
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
```

Student라는 key 값에 여러 object의 value를 가진다.

: 이러한 구조는 JSONArray 타입이다.

**JSONObject**

- key:value 쌍을 중괄호{ }로 담고 있는 객체 구조
- key value 구분은 :
- 그룹당 구분은 ,

**JSONArray**

- 배열 구조
- 대괄호 안에 값을 담고, comma(,)로 값을 분류
- index 사용 가능 (순서가 있다)

### JSONObject로 parsing하기

- **JSONObject Library**
    - 해당 라이브러리를 다운받으면 과정이 훨씬 간결해진다.
    - pom.xml에 라이브러리 다운

        ```
        <!-- for jason -->
            <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20201115</version>
            </dependency>
        ```

```json
{"info":{"size":{"width":223,"height":226},"faceCount":2},
"faces":[{"celebrity":{"value":"송중기","confidence":0.644043}},
				 {"celebrity":{"value":"이연희","confidence":0.188795}}]}
```

```java
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
```

- 코드 해석
    - String faceResult = (String)request.getAttribute("faceResult");

        →String type으로 받아오기

    - JSONObject obj = new JSONObject(faceResult);

        →JSONObject type으로 형변환 

    - Object imsi = obj.get("faces")

        →faces 배열값 가져오기 

    - for(Object cele : faces)

        →인식 값이 여러개일 경우를 대비한 반복문

    - JSONObject celebrity = (JSONObject) ((JSONObject)cele).get("celebrity");

        →JSONObject타입으로 변환하며 배열 안 원하는 key를 get

    - celebrity.get("value")

        →get한 key 배열 안 key값을 get

### Javascript로 parsing하기

```json
{"predictions": 
[{"num_detections": 1, "detection_classes": [1.0], 
"detection_names": ["person"], 
"detection_scores": [0.996668], 
"detection_boxes": [[0.0140925, 0.0131138, 0.971422, 0.797791]]}]}
```

```jsx
<%
	String result = (String)request.getAttribute("objectdetectionResult"); 
%>

$(document).ready(function(){
	$("#result").text('<%=result%>');
	var json = JSON.parse('<%=result%>');
	$("#count").text("객체탐지수 = " + json.predictions[0].num_detections + "개");
	$("#names").text("객체이름 = " + json.predictions[0].detection_names);
	$("#confidence").text("확률 = ");
	for(var i = 0; i < json.predictions[0].num_detections; i++){
		$("#confidence").append
		(parseInt(parseFloat(json.predictions[0].detection_scores[i])*100) + "%, ");
		}
```

- 코드 해석
    - $("#result").text('<%=result%>');

        :html body태그에 <div id='result'></div> 태그가 있음. 

        : .text()함수는 해당 태그 내부를 초기화시키고 지정한 값을 넣겠다. 

    - var json = JSON.parse('<%=result%>');

        :JSON.parse() 함수 → 해당 String을 JSONObject타입으로 변환

    - $("#count").text("객체탐지수 = " + json.predictions[0].num_detections + "개");

        :id가 count인 태그에 json 배열 첫번째값의 key값을 가져온다.