# DOM

Document Object Model (문서 객체 모델)

> 정적 페이지 HTML 태그를 읽고 기능을 추가해 동적을 바꾸기 위해 태그를 읽어올 때 태그들을 객체취급해서 자바스크립트 모델로 변환하는 것. 태그 안에 태그가 포함된 관계 



| html tag          | css                   | javascript                                                   |
| ----------------- | --------------------- | :----------------------------------------------------------- |
| 화면구성요소 나열 | 크기, 색상, 위치 결정 | 기능 추가                                                    |
| 정적 페이지 구성  |                       | 동적 페이지 구성<br />(=html 태그 변경 )                     |
|                   |                       | html태그를 읽고 기능 추가,<br />화면 동적 변경 <br />"태그"를 표현 데이터타입 객체 취급 <br />(document object model) |

##### document object

: 문서객체, 자바스크립트 안에 내장된 객체

##### nod

: 요소를 나타내는 것들, element node와 text node로 구분 

````html javascript
<script>//자동으로 생성
var body = { innerHTML : a, , , ,}
var a = {href : "www.daum.net",
         innerHTML : "링크",
         ... }
         //태그를 하나의 자바스크립트 객체로 취급하게 되어 있음. 
</script>
<body>
  <a href = www.daum.net>링크</a>
</body>
````







#### 실행순서 

> 자바스크립트에서 HTML태그를 읽어올 때, 태그 이전에 불러오면 null상태(실행 순서상 태그 앞에 존재하기 때문에 없는 태그), 이 경우 세 가지 옵션이 있다



* 오류의 경우

````html javascript
<html>
  <head>
    <title></title>
    <script>
      document.querySelector('h1').style.color = 'red'; 
      //실행 순서상 먼저 실행, 선택한 태그는 null상태 
    </script>
  </head>
  <body>
    <h1>제목입니다.</h1>
  </body>
</html>
````



1) HTML 코드 뒤에 태그

````html javascript
<html>
  <head>
    <title></title>
  </head>
  <body>
    <h1>제목입니다.</h1>
  </body>
   <script>
      document.querySelector('h1').style.color = 'red'; 
      //실행 순서상 먼저 실행, 선택한 태그는 null상태 
    </script>
</html>
````



2) window.onload

: 브라우저 창에 문서의 로딩이 완료되면 연결된 함수를 실행

````html javascript
<html>
  <head>
    <title></title>
    <script>
      window.onload = function(){
      document.querySelector('h1').style.color = 'red'; 
      }
      //실행할 코드를 function 안에 담아주면 된다. 
    </script>
  </head>
  <body>
    <h1>제목입니다.</h1>
  </body>
</html>
````



3) setTimeout

````html javascript
<html>
  <head>
    <title></title>
    <script>
      setTimeout(function(){
      document.querySelector('h1').style.color = 'red'; 
      }, 1000);
      //브라우저가 실행되고 1초 뒤에 실행 
    </script>
  </head>
  <body>
    <h1>제목입니다.</h1>
  </body>
</html>
````





#### 문서 객체 조작



##### 문서 객체 선택

| 메소드                          |                         |
| ------------------------------- | ----------------------- |
| document.getElementByID         | 아이디 한 개 선택       |
| document.querySelector          | 선택자 한 개 선택       |
| document.getElementsByName      | name 속성 여러 개 선택  |
| document.getElementsByClassName | class 속성 여러 개 선택 |
| document.querySelectorAll       | 선택자 여러 개 선택     |

	* querySelector 선택자 문법은 css를 따르면 된다. 
	* 여러 개 선택시 리턴은 배열타입, 반드시 인덱스를 기입해줘야 한다. 

````html javascript
<!DOCTYPE html>

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.onload = function(){
           document.querySelector("h1").innerHTML += "제목수정";
            // 기존의 내용 뒤에 추가할 것: +=, 수정: =
           document.querySelector("div").innerHTML += "<h3>수정</h3>";
           //복수의 태그를 하나로 선택시 첫번째 값이 불려온다.
           document.getElementByID("d").style.color = "blue";
           document.querySelectorAll("div")[2].style.backgroundColor = "yellow";
          // dom: css의 -대신 두번째 단어 시작을 대문자로
   				 }
	  </script>

</head>
<body>
    <h1>제목</h1>
    <div>추가합니다</div>
    <div id = "d">추가합니다2</div>
    <div>추가합니다3</div>
    <img>
</body>
</html>
````



##### 객체 조작

##### 글자 속성

> DOM내부에 글자를 조작하려고 할 경우 

| innerHTML   | 문서 객체 내부 글자를 순수 텍스트 형식으로 가져오도록 변경 |
| ----------- | ---------------------------------------------------------- |
| textContent | 문서 객체 내부 글자의 HTML 태그를 반영해 가져오도록 변경   |

````html javascript
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.onload = function(){
           for(var i = 1; i <= 10; i++){
                document.body.innerHTML += "<div> + i" + "번째 생성</div>";
             //body태그 내부에 추가 
            }
   				 }
	  </script>

</head>
<body>
    <h1>제목</h1>
    <div>추가합니다</div>
    <div id = "d">추가합니다2</div>
    <div>추가합니다3</div>
    <img>
</body>
</html>
````





##### 이미지 조작

````html javascript
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        var img_tag = document.querySelector("img");
        img_tag.src = "google.png";
        img_tag.width = 100;
        img_tag.height = 100;
   				 }
	  </script>
</head>
<body>
    <img>
</body>
</html>
````



##### 속성 조작

* setAttribute(속성 이름, 속성 값)
* getAttribute(속성 이름)

##### 

````html javascript
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        var img_tag = document.querySelector("img");
        img_tag.src = "google.png";
        img_tag.width = 100;
        img_tag.height = 100;
   				 }
           
        img_tag.setAttribute("user-difine", "이미지 보여줄게요");// 없는 속성 추가, 속성명, 추가할 항목
        alert(img_tag.getAttribute("user-define")); 
	  </script>
</head>
<body>
    <img>
</body>
</html>
````





# 이벤트

> 키보드를 누르거나 마우스를 클릭하는 등 프로그램에 영향을 미치는 것 

##### 이벤트 종류: 

| window-브라우저 창             | onload                                                  | html문서 로딩 완료 이벤트                          |
| ------------------------------ | ------------------------------------------------------- | -------------------------------------------------- |
| html모든 태그                  | onclick<br />ondbclick<br />onmouseover<br />onmouseout | 클릭/더블클릭/마우스오버/<br />마우스 아웃 시 실행 |
| input type = text/password     | onkeydown<br />onkeypress<br />onkeyup                  | 키보드 입력 시 실행                                |
| input<br />type=radio/checkbox | onchange                                                | 상태변화이벤트                                     |
| input type=submit              | onsubmit                                                | form양식 입력                                      |

	* 이벤트 이름: on을 제외한 이름
	* 이벤트 속성: onxxxx
	* 이벤트 핸들러: 이벤트 속성에 넣는 함수



````html javascript
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.onload = function(){
        //클릭버튼2라는 value를 가진 태그를 읽어와서 onclick 이벤트 주기
        var click1 = document.querySelector("#click1");
        click1.onclick = function(event){
            alert(event.target.tagName); //이벤트 이름 [object HTMLInputElement]
            alert(this.tagName);//위와 같은 의미 
            click1.value = "수정"
        }
    }
    </script>
</head>
<body>
   <input id = "click1" type=button value="클릭버튼2"><br>
</body>
</html>
````

* 이벤트 객체: 이벤트 객체 //function(event){}를 사용하면 이벤트와 관련된 정보를 알 수 있다. 





##### 버튼기능만들기

```` html javascript
<!DOCTYPE html>

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
  window.onload = function(){
             //링크정보 버튼 클릭
             var button = document.querySelector("#inform");
             var div = document.querySelector("#result");
             button.onclick = function(){
                 var a_list = document.querySelectorAll("a");
               
                 a_list.forEach(function(one){// a_list 개수만큼 알아서 반복하라 / callback
                    div.innerHTML += one.innerHTML + "-" + one.href + "<br>"
                 }); 
                }   
        }
    </script>
</head>
<body>
    <a href="http://www.multicampus.co.kr" target="_blank">멀캠으로 이동</a>
    <a href="http://www.google.co.kr" target="_blank">구글으로 이동</a>
    <a href="http://www.apple.co.kr" target="_blank">애플로 이동</a>
    <a href="http://www.daum.net" target="_blank">다음으로 이동</a>

    <form id = "f" action="a.jsp">
        <input type="text">
        <input type="submit" value="전송">
    </form>
    <button id = "inform"><b>링크정보</b></button>
    <div id = "result"></div>
</body>
</html>
````

+) 아래 두 표현은 같은 반복문

````javascript
for(var i = 0; i < a_list.length; i++){
 div.innerHTML += a_list[i].innerHTML + "-" + a_list[i].href + "<br>"
 }

a_list.forEach(function(one){
div.innerHTML += one.innerHTML + "-" + one.href + "<br>"
 }
````



##### 기존 동작 방지

:기능을 내장하고 있는 태그의 기존 기능을 없앨 수 있다. 

````html javascript
<!DOCTYPE html>

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.onload = function(){
            document.querySelector("a").onclick = function(e){//변수선언, e는 이벤트 객체 
                e.preventDefault(); //기본 동작 못하도록 방지. 
            }
            document.querySelector("#f").onsubmit = function(e){//변수선언, e는 이벤트 객체 
                e.preventDefault(); //기본 동작 못하도록 방지.    
            }
        }
    </script>
</head>
<body>
    <form id = "f" action="a.jsp">
        <input type="text">
        <input type="submit" value="전송">
    </form>
</body>
</html>
````



##### 표준이벤트 모델과 화살표 함수

* .addEventListner :

  *  여러개의 이벤트 핸들러를 등록 가능.
  * 하나의 이벤트 대상에 복수의 동일 이벤트 타입 리스너를 등록
  * 복수의 엘리먼트에 하나의 리스너를 등록해서 재사용 가능

* 표준 이벤트 모델

  ​	

* 화살표 함수

  ​	(매개변수) ==> {문장}

````html javascript
<!DOCTYPE html>

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.onload = function(){
           //mouse 이동시 색상변경, 표준이벤트 모델 
          
           document.querySelector("#mousetest").addEventListener
           ("mouseover", ()=>{ // 화살표함수
               document.querySelector("#mousetest").style.backgroundColor = "green";
           } );
          
           document.querySelector("#mousetest").addEventListener
           ("mouseout", function(){
               document.querySelector("#mousetest").style.backgroundColor = "green";
           } );
        }
    </script>
</head>
<body>
    <div id = "mousetest">마우스 올려보세요</div>
</body>
</html>
````



