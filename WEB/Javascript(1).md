# Javascript

> html, css가 웹의 정적 요소라면, 웹페이지를 동적으로 제어할 수 있는 언어가 Javascript이다.



#### 설정방식

* inline 방식

````javascript
<h1 onclick="javascript:alert(클릭)">제목클릭</h1>
  //거의 쓰이지 않는 방식
````

* html파일 내부 작성

````javascript
<html>
  <head>
   <script>
  		......
   </script>
	<head>
 <html>
 
````

​		* 스크립트태그는 <head>내부에 반드시 작성하지 않아도 된다. <body>나 <head>나 어느 위치든 상관 없음.

* 외부 파일 작성

````javascript
<script src="a.js">
  </script>
````





##### Java와 Javascript의 기본 문법 차이

|                      | Java | Javascript           |
| -------------------- | ---- | -------------------- |
| 대소문자 구분        | O    | X                    |
| String 타입          | " "  | " " / ' ' 둘 다 가능 |
| 변수 데이터타입 설정 | O    | X                    |

* 연산자와 조건문, 반복문은 모두 같다 



#### 변수선언

* 변수 선언은 **var**/let/const
  * 변수 type은 정하지 않음. 변수에 다양한 타입 가능, 값을 정해야 타입이 정해짐 
    * 변수가 선언되면 우선적으로 메모리 영역이 확보된다. 

````javascript
var a = 10;
var a = "열"
//var는 여러 변수 선언이 가능

let f = 3.14;
//let은 변수 선언이 중복되면 오류

const h = 100;
h = 200; //오류 
//const는 상수, 변수 할당시 오류
````

* type
  * 정수, 실수 구분이 없음. 기본적으로 number 타입
  * == 연산자 비교시, type은 따지지 않고 모양만 비교, 모양이 같으면 true

````javascript
document.write(10/3 + "<br>"); //3.333 
document.write(typeof(10/3) + "<br>");//number
document.write(parseInt(10/3) + "<br>");//자바와 달리 정수타입 실수, 문자열 모두 parseInt

 var a= 10; 
 var b= 10.0;
 var c= "10.0";
document.write((a == b) + "<br>");// true
document.write((a == c) + "<br>");// true
//연산자 === : type과 값을 같이 따짐
document.write((a === b) + "<br>");//true
document.write((a === c) + "<br>");//false
````



* **this**

function 내부에 멤버변수를 사용할 경우, 그 변수가 멤버변수라는 것을 알리기 위해 this를 사용한다. 지역변수와 이름이 겹치지 않더라도, 반드시 표시한다. (Java와 차이가 있음)

````JavaScript
var product = {
                code : 100,
                name : '멀티컴퓨터',
                price : 1000000,
                detail : '자세한 상품정보',
                images : ['pr1.jpg', 'pr2.jpg', 'pr3.jpg'],
                calcPrice : function(sale){
                    this.price = this.price * (1-sale); 
                    return this.price;
                }
            };
````



#### 배열

* Java와 달리 배열 선언시 type을 지정하지 않음. 배열에 여러 타입이 올 수 있다.
* 배열 길이 또한 선언시 지정하지 않아도 됨, 유동적 배열

배열 선언

````javascript
 var ar2 = new Array();
````

````javascript
var ar1 = [1, "java", true, 200.99, "300"]

ar1.push(100); //배열의 마지막 값에 100을 추가
ar1.unshift(200); //배열의 첫번째 값에 200을 추가
ar1.pop(); //배열의 마지막 값 삭제
ar1.shift(); //배열의 첫번째 값 삭제
````

* 반복문

````JavaScript
for(var i = 0; i < ar1.length; i++){
                document.write(ar1[i] + "<br>");
            }
//아래는 위와 같음
document.write(ar1 + "<br>");
//js는 반복문이 없어도 배열 출력이 가능. 기본 구분자 ,(comma)로 출력
document.write(ar1.join("/") + b);
//join은 구분자를 주는 것 
````



* 예제, html 태그 불러와서 활용

````html JavaScript
<body>
<h1>과일을 고르세요</h1>
	<form name="f">
 <input type="checkbox" name="fruit" value=""> <span></span>
 <input type="checkbox" name="fruit" value=""> <span></span>
 <input type="checkbox" name="fruit" value=""> <span></span>
 <input type="checkbox" name="fruit" value=""> <span></span>
 <input type="checkbox" name="fruit" value=""> <span></span>
 <input type="checkbox" name="fruit" value=""> <span></span>
	</form>
      
 <script>
    var fruit = ['딸기', '사과', '바나나', '포도', '귤', '오렌지'];
    var input_list = document.getElementsByTagName("input"); 
   	// tag 읽어오기
    var span_list = document.getElementsByTagName("span"); 
   	// tag 읽어오기
            
    for(var i = 0; i < input_list.length; i++){
                input_list[i].value = fruit[i];
      					//첫번째 input 태그의 value 속성
                span_list[i].innerHTML = fruit[i];
            }
            
            
 </script>
</body>
````



#### 함수(Function)

Javascript에서 함수는 일종의 객체. 변수 선언 가능, 배열 내의 하나의 객체로도 가능.

* Javascript의 함수는 선언적 함수와 익명 함수가 있다.

  * 선언적 함수: 모든 자바스크립트 코드 실행 전 메모리 로드

  * 익명 함수:  변수 선언 시작하면 메모리로드
    * 익명함수에 변수 선언이 가능

  ````JavaScript
  var f1 = function(){ //3
                  alert("C")
                  return 10;
              } //익명함수 
  
              function f1(){ //1
                  alert("A")
              }
  
  						function f1(){ //2
                  alert("B")
              }
  ````

  실행 순서에 주의한다: 

  선언적 함수는 선언 전 메모리에 로드되고, 익명함수는 스크립트 코드가 실행되면서 메모리로드가 된다. 따라서 순서상 A 메모리 로드 > 2. B 로 내용 변경 > 3. 익명의 함수를 변수 이름으로 쓰면서, C로 변경. 최종적으로 출력되는 것은 "C"이다. 



* setTimeout

```JavaScript
<script>
function f1(){
      var div_list = document.getElementsByTagName("div");
  		//div .getElementsByTagName는 태그를 하나더라도 배열로 만들어옴
      var date = new Date();
      //var datestring = date.getLocaleDateString();
      div_list[0].innerHTML = date;
             }
      //setTimeout(f1, 5000);//setTimeout(함수내용, int타입(초));
      //f1을 5초 뒤에 실행하라. 태그 위치보다 먼저 실행하고 있더라도, 먼저 실행되지 않음. 
      var timer_id = setInterval(f1, 1000); 
			//1초마다 한 번씩 f1함수를 실행 (시간이 1초마다 업데이트 됨 시계처럼)
      setTimeout(function(){clearInterval(timer_id)}, 10000); 				//10초 후에 한 번만 익명함수를 실행하라
       </script>
```



* **call back**

  : 다른 함수의 매개변수로 전달되는 함수

  : 함수를 변수처럼 취급하기 때문에 함수 내에 함수가 가능. 일종의 지역변수같은 것.

````JavaScript
function f1(arg){
	arg();
	var inner = function(){  }
	return function(){ }
  //return값에도 함수가 들어갈 수 있다. 
} 
````

```javascript
// f함수를 이용하여 "html"을 n번 출력하라 
function manytimes(f, n){
                for(var i = 1; i <= n; i++){
                    f("html");
                }
            }     
            function print(message){
                document.write("<h1>" + message + "<h1>");
            }
            manytimes(print, 8);
            vartest();

```



* 호출시

  * 매개변수 오류

  ````JavaScript
  var f1 = function(e, f) { return e / f; }
  
  var result = f1();//error
  var result = f1(1); // error
  var result = f1(1, 2); // ok
  var result = f1(1, 0); // error 결과값 0
  var result = f1("html", "css") // error
  var result = f1(1,2,3); ok
  //매개변수 넘치는 것은 상관 x (넘친느 것은 알아서 사용하지 않음) 
  //그러나 값이 적합하지 않으면(나눌수 없거나, 나누면 0) 에러. 
  ````

  * 함수 호출시 매개변수로 함수 가능

  ````JavaScript
  f1(function(){ 
  ...
   }); 
  ````



#### 객체(Object)

* 객체 생성

````JavaScript
var 객체변수명 = {
속성변수명2: 값2, 
속성변수명2: 값1,
....속성변수명3: function(){..}
 };
````

​	속성: 객체에 있는 값 하나하나

​	블럭 안에 있는 내용들에 변수를 준다. 여러개일 경우 ,(comma)로 구분을 준다. 

````javascript
<script>
            var product = {
                code : 100,
                name : '멀티컴퓨터',
                price : 1000000,
                detail : '자세한 상품정보',
                images : ['pr1.jpg', 'pr2.jpg', 'pr3.jpg'],
                calcPrice : function(sale){
                    this.price = this.price * (1-sale);
                    return this.price;
                }
            };
        </script>
````



예제 )

````html JavaScript
<html>
    <head>
        <title></title>
        <meta charset="UTF-8">
    </head>
    <body>
        <script>
        var inform = prompt();
        var inform_list = inform.split(' ');

        var student = {
            name : inform_list[0],
            kor : inform_list[1],
            eng : inform_list[2],
            mat : inform_list[3],
            sum : 0,
            avgFloat : 0,
            avgInt : 0,
            grade : '',
            calc : function(){
                this.kor = parseInt(this.kor);
                this.eng = parseInt(this.eng);
                this.mat = parseInt(this.mat);
                this.sum = this.kor + this.eng + this.mat;
                this.avgFloat = this.sum / 3;
                this.avgInt = parseInt(this.avgFloat);
            },
            getGrade : function(){
                if(this.avgInt >=90){
                    this.grade = "A";
                }else if(this.avgInt >= 80){
                    this.grade = "B";
                }else if(this.avgInt >= 70){
                    this.grade = "C";
                }else if(this.avgInt >= 60){
                    this.grade = "D";
                }else{
                    this.grade = "F";
                }
            },
            toString : function(){
               return "이름 = " + this.name + "<br> 국어 =" 
               + this.kor + "<br> 영어 =" + this.eng
               + "<br> 수학 =" + this.mat + "<br>총점 =" + this.sum
               + "<br> 실수평균 =" + this.avgFloat + "<br> 정수평균 =" 
               + this.avgInt + "<br>등급 =" + this.grade;
            }
        };
        
       // document.write(student + "<br>");
        student.calc()
        student.getGrade();
        document.write(student);
      //  student.toString
    </script>
    </body>
</html>
````





#### JASON

: JavaScript Object Notation라는 의미의 축약어로 데이터를 저장하거나 전송할 때 많이 사용되는 경량의 DATA교환 형식

: Javascript에서 객체를 만들 때의 표준식 (텍스트 형식이다.)

* <u>속성 변수 타입</u>을 줄 때, 이름은 무조건 <u>" "(이중따옴표)를 사용</u>한다. 
* 숫자타입과 true/false는 별다른 표기를 하지 않고 <u>문자열데이터인 경우에는 " "(이중따옴표)를 사용</u>한다. 

````JavaScript
{
"속성변수명1" : 100
"속성변수명2" : true
"속성변수명3" : "javascript"
"함수명1" : function(){...}
}
````



* Javascript객체를 JASON으로 변환하는 함수

````javascript
 var json_student = JSON.stringify(student);
 document.write(json_student+"<br>"); 
 // 함수를 실행한 결과값만 적용. 변수 이름의 값만 저장.

 var origin_student = JSON.parse(json_student);
 //원래의 텍스트 형식 보기 
 document.write(origin_student.name+"<br>");
 document.write(origin_student.grade+"<br>");
 // parse를 쓸 경우, 변형할 변수명을 알려줘야 한다. 
````

