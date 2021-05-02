# jQuery

> Javascript를 간결하고 이해하기 쉬운 구조로 만들어주기 위해 자바스크립트의 기본 문법으로 라이브러리를 생성, 그 기본 라이브러리 중 하나가 jQuery. 라이브러리는 받아서 써야 한다. 



jQuery 사용 베이스

* <head> 태그에 쓸 경우

````html javascript
<!DOCTYPE html>
<head>
<script src="jquery-3.2.1.min.js"></script>
<script>
  $(document).ready(function(){ //브라우저에 출력된 이후 실행
    
  });
</script>
</head>
````

jquery를 다운받아서 경로를 표시 혹은 웹 주소로 표시. 후자의 경우 인터넷 연결 상태 필수 





* 자바스크립트에 변수, 함수가 다 놓여있다면, 제이쿼리는 함수만 있다

  ​	$("jQuery 태그선택자 - css selector").jquery 함수(매개변수)

````javascript
 document.querySelector("h1").style.color = "orange;"

 $('h1').css("color", "orange")
````

* 기존의 document 객체를 불러오는 대신에 $ 달러사인으로 대신한다



#### $("css선택자").jQuery함수()

| document.querySelector("css선택자").style.color = "red"      | $("css선택자").css("color", "red")<br />$("css선택자").css("color") : 요소 선택방법 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| document.querySelector("css선택자").innerHTML                | $("css선택자").html("문자") : setter<br />$("css Sel").html( ) : getter |
| document.querySelector("css선택자").textContent              | $("css Sel").text("문자")<br />$("css Sel").text( )          |
| document.querySelector("css선택자").태그 서로 다른 속성 = xx | $("css Sel").attr("src", "a.png")<br />$("css Sel").attr("src") |





#### 문법

1. this

* this는 자바스크립트의 this의 의미와 같으나 jQuery에서 사용시 $(this) 문법으로 바꿔서 사용한다.

````javascript
$(" ").on('이벤트명', function(){
$(this) // 여기서 this는 해당 선택자로 선택한 것을 의미 
})
````

````javascript
$("h1").css("color", "red").on('click', function(){
                $(this).css("border", "solid 3px red"); 
              // 작동이 여러개인 경우 this로 바꾸면, 클릭한 것만 바뀐다. this는 내가 선택한 <h1>태그
            });
````



2. .val

* 자바스크립트의 value. 해당하는 value의 값을 읽어오는 역할, jQuery에서는 .val() 로 사용한다.

````javascript
$("input[type=text]").val() 
//<input type = text>에 입력된 값을 가져온다. 
````





### 이벤트

jQuery의 경우 이벤트 종류가 이벤트 함수 이름 그대로 사용된다. (즉 on이 없음)

````javascript
$("css선택자").click(function(){ .... });
````

그리고 이 함수는 아래와 같이 변경이 가능하다.

````javascript
$("css선택자").on('click', function(){ ..... })
````

* 해당 함수가 이벤트 함수라는 것을 암시하기 위해 .on이 붙은 이벤트함수형태를 사용하는 것이 지향된다. 



예제) 이벤트 함수의 다양한 예제

````javascript
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="jquery-3.2.1.min.js">
    </script>
    <script>
        $(document).ready(function(){
            //함수 연결 사슬고리 ( method chain ) 연결해서 사용도 가능
            $("h1").css("color", "red").on('click', function(){
                $(this).css("border", "solid 3px red"); 
              // 작동이 여러개인 경우 this로 바꾸면, 선택한 것만 바뀜. this는 내가 선택한 <h1>태그. 
            });
            $("#first").on("mouseover", function(){
                $(this).css("background-color", "skyblue");
            });
            $("#first").on("mouseout", function(){
                $(this).css("background-color", "pink");
            });
            $("button").on("click", function(){
                $("h1").off("click"); //클릭 동작 중지
            });

            $("#one").one("click", function(){
                alert(1); // one함수는 한 번만 작동하고 더 하지 않음
            });

            $("a").on("click", function(e){
                e.preventDefault();
                $(this).css("text-decoration", "none");
                $(this).css("color", "yellow");
            });

            $("#btn_new").on("click", function(){
                $('#result').append("<button id = 'after1'>추가버튼</button>")
            })

            //동적 추가 버튼 클릭시, 동작하게 하기 > 부모태그 선택
            $("#result").on('click', '#after1' ,function(){
                alert("추가버튼 클릭");
            });
            //result영역에 새로 생긴 after1에 click버튼을 누르면 function을 실행하라. 
        });//ready end


    </script>
</head>
<body>
    <h1>Click me</h1>
    <h1>Click me 2</h1>
    <div id = "first"> Mouse on here </div>
    <button id = "stop"> 동작 그만 </button>
    <button id = "one"> 한 번만 동작 </button>
    <a href="http://www.daum.net">다음으로 이동</a>
    <button id = "btn_new">버튼생성</button>
    <div id = "result"></div>
</body>
</html>
````



* keyup

  : 키보드 입력에 관련된 이벤트 작성이 가능하다 

  : e.KeyCode 해당 값을 읽어오기 위해서 함수에 변수값을 주고 읽어오면 된다. 

  * fucus() : 자동 입력상태 

````javascript
<!DOCTYPE html>

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src ="jquery-3.2.1.min.js"></script>
    <script>
        $(document).ready(function(){
            $("textarea").focus(); // 마우스 클릭 없이, 바로 입력 가능. 자동 입력 가능 상태로 만들기 
            // 10글자 넘어가면 더 이상 입력 금지 
            $("textarea").on('keyup', function(){
                var input_len = $(this).val().length;
                var remain_len = 10 - input_len;
                $("h1").text(remain_len);
                $("h2").text(" 글자 남았습니다.")
                if(remain_len < 0){
                    $(this).attr("readonly", "readonly");
                    $("h1").css("color", "red");
                }
            });
        })
    </script>
</head>
<body>
    <h1> 10 </h1>
    <h2> 글자 입력 가능합니다. </h2>
    <!--10글자를 넘어가면 더이상 입력 안 되게 하기-->
    <textarea rows="5" cols="100"></textarea> 
    
    </textarea>
</body>
</html>
````



* 추가 함수 

  empty() : 특정 태그 내부 내용들을 삭제

  remove() : 특정 태그 모두 삭제

  hide() : 감추기

  show() : 보이기

  

* 해당 이벤트에 변수값을 줘서 내용을 읽어오거나 기능 없애기 및 이벤트버블링금지

  ````javascript
  $(" ").on('이벤트명', function(event){ // 해당 이벤트 내용을 가져올 수 있음
  
  event.target.tagName
  
  event.X
  
  evetn.Y
  
  event.preventDefault() // 기능없애기
  
  event.keyCode
  
  event.stopPropagation() //이벤트 버블링 금지
  
  })
  ````





* 이벤트 버블링 

  : 이벤트는 기본적으로 안 쪽에 있는 태그부터(가까운 쪽 먼저 실행) 바깥쪽으로 퍼져나간다. 이벤트 버블링은 기본적으로 자바스크립트나 제이쿼리가 기본적으로 처리하는 방식을 보여주는데, 부모태그와 자식태그의 경우 자식 태그가 먼저 실행된다. 

  *  이벤트 버블링을 안 하도록 처리하려고 사용하는 것이 

     event.stopPropagation()

````javascript
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="jquery-3.2.1.min.js"></script>
    <script>
        $(document).ready(function(){
            //이벤트가 전파, 자식태그가 먼저 출력 
            $("h1").on('click', function(){
               // alert(1);
                $(this).css("background-color", "red");
            });

            $("div").on('click', function(e){
                $(this).css("background-color", "yellow");
                $(this).css("width", "200px");
                e.stopPropagation();// 버블링 이벤트 처리 막기 
            });
        });
    </script>
</head>
<body>
  <!--   <h1><div>클릭합니다.</div></h1> -->
</body>
</html>
````



* 애니메이션 효과 주기(시간차로 사진나타내기)

````javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="jquery-3.2.1.min.js"></script>
    <script>
        $(document).ready(function(){
            // 이미지 추가 
            var img_list = ["/html/images/americano.jpg", 
                            "/html/images/blackcoffee.gif", "/html/images/cafelatte.jpg", 
                            "/html/images/cappuccino.jpg", "/html/images/coffee.gif"];
            for(var i = 0; i < img_list.length; i++){
              var f1 = function(index){

               setTimeout( function(){
                   $("#image").append("<img src = " + img_list[index] + " width=200 height = 200>");
                } , (i+1)*1000 );
            }
            f1(i);
         } 
        });
    </script>
</head>
<body>
    <div id = "image">
    <img src = "/html/images/android.jpg" width="200" height="200">
    <img src = "/html/images/chrome.jpg" width="200" height="200">
    <img src = "/html/images/google.png" width="200" height="200">
    </div>    
</body>
</html>
````







예제

````javascript
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="jquery-3.2.1.min.js">
    </script>
    <script>
        //value가 아메리카노면 배열에 맞춰서 가격이랑 곱하기 
        //주문완료 버튼을 누르면 계산, 
        var drink_price_list = [2500, 3000, 4000, 3500, 3000];
        var drink_name_list = ['아메리카노', '카페라떼', '카푸치노', '우유', '코코아']
        var bread_price_list = [4500, 3000, 7000, 6000];
        var bread_name_list = ['스콘', '베이글', '샌드위치', '치즈케잌'];

        $(document).ready(function(){
            $('form').on('submit', function(e){
                e.preventDefault();
                var totalprice = 0;
                var drink_name = $("input[type=checkbox]:checked").val()
                var drink_amount = $("input[type=text]:first").val();
                for(i = 0; i < drink_name_list.length; i++){
                    if(drink_name == drink_name_list[i]){
                        totalprice = drink_price_list[i]*drink_amount;
                    }
                }//for end
                var bread_name = $("select option[selected]").val();
                var bread_amount = $("input[type=text]:last").val();
                for(i = 0; i < bread_name_list; i++){
                    if(bread_name == bread_name_list[i]){
                        totalprice = totalprice + bread_price_list[i]*bread_amount;
                    }
                }//for end 

                $("#order").append(drink_name + "-" + drink_amount + "<br>")
                $("#order").append(bread_name + "-" + bread_amount + "<br>")
                $("#order").append(totalprice + "<br>")

            });
            $("input[type=text]").on("keyup", function(e){
                //0-9 -48~57코드 키보드로 입력한 키 값(코드값)을 알아올 수 있음.
                if(e.keyCode > 57 || e.keyCode < 48){
                    $("#order").html("<h1>숫자만 입력 가능</h1>").css("color","red");
                }
            });
        });//ready end
    </script>
</head>
<body>
    <h1>음료 선택하세요</h1>
    <form action="order.jsp">
음료:
    
    <input type="checkbox" value="아메리카노"> 아메리카노<br>
    <input type="checkbox" value="카페라떼"> 카페라떼<br>
    <input type="checkbox" value="카푸치노"> 카푸치노<br>
    <input type="checkbox" value="우유"> 우유<br>
    <input type="checkbox" value="코코아"> 코코아<br>   
  
수량:
    <input id ="dn" type="text"><br>

디저트:
    <select>
        <option>스콘</option>
        <option>베이글</option>
        <option selected>샌드위치</option>
        <option>치즈케익</option>
    </select>
수량:
     <input id ="bn" type="text"><br>

     <input type="submit" value="주문완료"><br>
    </form>
    <div id="order">주문내역과 총 지불 가격 표시</div>
 
</body>
</html>
````

