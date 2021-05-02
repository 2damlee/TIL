# CSS

> Cascading Style Sheet
>
> : 크기, 모양, 색상, 배치위치를 결정하는 것을 정해놓은 sheet. html이 화면 구성이라면, css는 부가적인 요소들을 꾸며준다.



**설정방식**

1) <style>태그로 설정

````css
<style>
  h1          {color: red;}
  css 선택자(selector){ 
    css 요소명 : css값
    css 요소명2 : css값2; 
    css 요소명3 : css값3;
  	}
</style>
/*style 태그 내에 있는 항목들이 변경된다*/
````



2) inline방식

````css
<h1 style="color : red; "> 제목입니다 </h1>
/*각 html요소별 적용 가능*/
````



3) 외부 css파일에 stylesheet 적용

```css
<head>
  <link re = "stylesheet" href = "test.css">
  ...
</head>
/*여러개의 html파일이 하나의 css파일을 적용하게 될 때
```



#### 선택자

> html의 요소 하나, 혹은 요소들의 덩어리를 stylesheet으로 바꿔줘야 하기 때문에 <div id = " ">(*기능은 없지만 묶어주는 타입) 등의 이름을 불러와서 스타일 지정을 해줘야 함

| 종류      | 기능                                                         |
| --------- | ------------------------------------------------------------ |
| *         | html 내부 모든 태그 선택                                     |
| #아이디명 | 특정 id(이름)을 갖고 있는 태그 선택. *id속성은 중복되면 안 된다. |
| .클래스명 | 특정 클래스 태그 선택(클래스는 특정한 태그를 선택할 때 쓰인다) |



| 형태                                                      | **기능**                                       |
| --------------------------------------------------------- | ---------------------------------------------- |
| **선택자[속성 = 값]**<br />ex. input[type="text"]{ 요소 } | 특정한 속성 내부 값이 특정 값과 같은 태그 선택 |



* 후손 선택자 자손 선택자

| 부모>자손        | 직접적으로 포함되어 있는 요소        |
| ---------------- | ------------------------------------ |
| 부모 (공백) 후손 | 직접적이지 않아도 포함되어 있는 요소 |

+

| 이름:first-child     | '이름' 안에 속한 것 중 가장 첫번째에 있는 것 |
| -------------------- | -------------------------------------------- |
| 이름:last-child      | '이름' 안에 속한 것 중 가장 마지막에 있는 것 |
| 이름:nth-child(2n+1) | 배수정보 활용 가능                           |



#### 박스 속성

![스크린샷 2021-04-01 오전 11.14.52](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-01%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.14.52.png)

| 속성    | 설명                                                         |
| ------- | ------------------------------------------------------------ |
| margin  | 테두리와 다른 태그 사이의 테두리 바깥쪽 여백                 |
| border  | 테두리                                                       |
| padding | 테두리와 글자 사이의 테두리 안쪽 여백, 배경색 지정은 padding영역까지 적용 |
| width   | 글자를 감싸는 영역의 가로크기                                |
| height  | 글자를 감싸는 영역의 세로크기                                |

* 테두리나 여백 지정은 상하좌우 각각 다르게 지정 가능, 나열식(50px 40px 20px 10px). 순서는 왼쪽 위-오른쪽 위-오른쪽 아래-왼쪽 아래의 시계방향







#### 박스 속성

![스크린샷 2021-04-01 오전 11.14.52](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-01%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.14.52.png)

| 속성    | 설명                                                         |
| ------- | ------------------------------------------------------------ |
| margin  | 테두리와 다른 태그 사이의 테두리 바깥쪽 여백                 |
| border  | 테두리                                                       |
| padding | 테두리와 글자 사이의 테두리 안쪽 여백, 배경색 지정은 padding영역까지 적용 |
| width   | 글자를 감싸는 영역의 가로크기                                |
| height  | 글자를 감싸는 영역의 세로크기                                |





#### 박스 속성

![스크린샷 2021-04-01 오전 11.14.52](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-01%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.14.52.png)



#### css요소

| 글씨     | font-size / font-family / text-decoration / text-overflow    |
| -------- | ------------------------------------------------------------ |
| 색상     | color / border-color / background-color                      |
| 크기     | width / height                                               |
| 여백     | margin / padding                                             |
| 좌표     | top / left / right / bottom                                  |
| 배치규칙 | position-static\|relative\|albsolute\|fixed\|sticky<br />\|display-none\|block\|inline-block\|float-left/right\|z-index(큰값 우선) |



**가시속성**

| 키워드       | 설명                             |
| ------------ | -------------------------------- |
| none         | 화면에 드러나지 않음             |
| block        | 블록 박스 형식                   |
| inline       | 인라인 박스 형식                 |
| inline-block | 블록과 인라인의 중간 형태로 지정 |



**위치 속성**

| 키워드   | 설명                                                        |
| -------- | ----------------------------------------------------------- |
| absolute | 절대 위치 좌표 설정                                         |
| fixed    | 브라우저 화면을 기준으로 절대 위치 좌표 설정(스크롤시 부동) |
| relative | 원래 배정 위치에서 상하좌우로 위치 이동                     |
| static   | 위쪽에서 아래쪽 순서대로 배치                               |





#### 반응형 웹

> 반응형 웹 페이지는 미디어 쿼리를 사용해 개발 

* meta = "viewport" 필히 지정 

````html
<html>
<head>
	<meta charset='UTF-8' >
	<meta name="viewport" 
				content="width=device-width, 
								 initial-scale=1.0,
								 user-scalable=no"> 
<!--화면 조정시, meta에 반드시 viewpoint. meta 여러개 가능.content는 규격 맞추기 -->

  <!-- <meta name="viewport" 
content="width=device-width, 
initial-scale=1.0,
user-scalable=no, 
maximum-scale=1.0, 
minimum-scale=1.0"> -->
  <style>
  @media all and (max-width:800px) {
																		h1, table { margin:auto;}
																		body {background-image: none;}
																	}
  </style>
````









##### 예제코드

1) 선택자

````css html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <style type="text/css">
         h1{color: antiquewhite;} h1 "태그선택" */
         * {color: red;}  /*별은 모든 태그*/
         #first {color: burlywood;} 
         .redgroup {color:crimson} class redgroup인 태그 선택 */
         input[type=text] {color: darkcyan;} */
        input[name] {color:darkkhaki}*/
         body a {color:red;}  - */
         body > a {color:red;} /*바디 안에 직접 포함되어 있는 것*/

        /*
        자손 : 직접적으로 포함되어 있는 요소 : 부모 > 자손
        후손 : 직접적이지 않아도 일단 포함되어 있는 것 : 부모 (공백) 후손
        */
         h1:hover {color: deepskyblue;} /*마우스를 올리면 색 변화*/
         h1:active {color:darkorange;} /*h1을 클릭 한 상태일 때, 활성화/ 순서 주의*/
        input[type=radio]:checked {color:fuchsia;}/*안 됨*/
        option[selected] {color: fuchsia;}/*안 됨*/
        option:nth-child(2n) {color: aquamarine;} /*2의 배수가 되는 것만 색을 바꾸라*/ 
        option:first-child {color: blueviolet;}  */
        h1{display: none;}
        div#Upper {background-color: dimgray;/*#00(red)00(green)00(blue);*/
            /*width: 300px; /*배경 영역을 조정할 수 있음. pixel단위*/
            width: 300px; /*가로 크기는 전체 브라우저의 반만 차지*/
            height: 100px;
            font-size: 2em; /*지정하지 않으면 브라우저는 기본으로 16px 2em은 기본의 2배*/
            /*border: solid 10px rgb(193, 197, 242);/*선종류|두께|선색상*/
            border-style: dotted;
            border-width: 7px;
            border-color:dodgerblue;
            border-radius: 60px;
            margin: 20px;/*바깥여백 = top, bottom, right, left값이 모두 같을 경우 margin에 통합해 지정해도 된다*/
            padding: 50px;
             /* display: block한 줄에 하나씩*/
            }
         #Lower div /*순서에 따라 의미가 다르다. #Lower div > Lower에 포함된 영역을 div로 바꾸라*/
            {display: inline;}
        /*
        css 작성 순서 주의, 
        div#lower id가 lower인 div 태그
        #lower div: id lower인 태그의 자식 중 div 태그 
        block - 1줄에 1개 요소를 배치 (사방)
        inline - 1줄에 여러 개 요소를 배치 (왼-오 순서로 배치)
        자바 오라클이 내용물을 생성하는 것이라면, html css는 화면 구성에 관련된 것
        */
        body{
            background-image: url('google.png') ;
            background-repeat: no-repeat;
            background-size: 50% 150px;      
        }
        #first{
            font-size: larger;
            font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
            font-style: italic;
            text-decoration: underline;
        }
        a{
            color:dodgerblue;
            text-decoration: none;
            font-size: x-large;
        }
        #align{
            background-color: rgb(242, 208, 19);
            width: 400px;/*브라우저 전체 크기->200px로 크기 줄이기*/
            text-align: center; /*글씨정렬*/
            margin: auto;/*브라우저가 알아서 정렬*/
            text-shadow: 5px 5px 5px slategray;
            box-shadow: 5px 5px 5px royalblue;
        }
        </style>
    </head>
    <body>
    <div id ="Upper">
        <div> div 태그 영역입니다 </div>
    </div>
        <h1 id="first">첫번째 제목</h1> <!--id에 준 name은 하나만 줘야 한다. 다른 태그와 중복된 값을 주면 안 됨.-->
        <p id="first">p 태그는 하나의 문단을 표현합니다. abcdefghij</p>
        <div id="align">정렬 테스트 중입니다.</div>
        <a class="redgroup" href="/boardlist.html">이동</a>
        <h1><a class="redgroup" href="/boardlist.html">이동</a></h1>
        <p class="redgroup">p 태그는 하나의 문단을 표현합니다. 두번째 </p>
        <!--class는 그룹 이름 -->
        아이디 입력 <input type="text" name="id" value="아이디입력칸"> <!--입력 초기 값이 none-->
        암호 입력 <input type="text" value="none"><br>
        이름 입력 <input type="text" value="이름입력칸"><br>
        성별<input type="radio" name="gen" value="남">남자
           <input type="radio" name="gen" value="여" checked="checked">여자 <!-- 체크 하지 않은 상태에서, default값 checked--> <br>
           <select>
               <option> 첫번째 </option>
               <option selected="selected"> 두번째 </option>
               <option> 세번째 </option>
               <option> 네번째 </option>
               <option> 다섯번째 </option>
               <option> 여섯번째 </option>
           </select>
         
         <div id ="Lower"><!--div의 용도-->
           <div> 아래쪽 div1 </div>
           <div> 아래쪽 div2 </div>
           <div> 아래쪽 div3 </div>
        </div>
    
        </body>
</html>
````



2) position1

````html css
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <style>
        .box{
            display: inline-block;
            width: 100px;
            height: 100px;
            background: slateblue;
            color: white;
        }
        #two{
            position: relative;/*two가 원래 있던 자리에서 얼만큼 떨어져 있는지*/
            top: 10px;
            left:10px;
            background-color: thistle;
        }
        #three{
            position: absolute;/*브라우저 왼쪽 상단을 기준으로 떨어진 거리: 좌표 기준-브라우저상단(원래는 부모태그)*/
            top: 30px;
            left: 30px;
            background-color: olive;
        }
        
    </style>

<body>
    <div class="box" id="one">One</div>
    <div class="box" id="two">Two</div>
    <div class="box" id="three">Three</div>
    <div class="box" id="four">Four</div>
</body>
</html>
````



3) position2

````html css
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
<style type="text/css">
.box {
  width: 100px;
  height: 100px;
}

#one {
  position: fixed;/*화면에서 동일한 위치를 벗어나지 않음.*/
  top: 80px;
  left: 100px;
  background: blue;
}

 #two { 
position: sticky; /*화면에서 사라질 때 고정*/
top: 10px; /*top으로부터 10px이 마지노선*/
background: pink;
} 

.outer {/*클래스 이름이 outer > .outer*/
  width: 500px;
  height: 300px;
 /* overflow: scroll;/*정한 크기에서 내용이 초과하면 scrollbar를 생성*/
  padding-left: 150px;
}
/*글 줄이기*/
.outer p {
  white-space: nowrap;
  overflow: hidden;/*정한 크기에서 내용이 초과하면 감춤*/
  /*nowrap: <br>태그만 줄바꿈, 길어진 내용 그대로 한줄로 표현
  wrap: <br>태그도 줄바꿈, 길어진 내용 자동으로 줄바꿈*/
  text-overflow: ellipsis;
}
</style>
</head>
<body>

<div class="outer">
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam congue tortor eget pulvinar lobortis.
    Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Nam ac dolor augue.
    Pellentesque mi mi, laoreet et dolor sit amet, ultrices varius risus. Nam vitae iaculis elit.
    Aliquam mollis interdum libero. Sed sodales placerat egestas. Vestibulum ut arcu aliquam purus viverra dictum vel sit amet mi.
    Duis nisl mauris, aliquam sit amet luctus eget, dapibus in enim. Sed velit augue, pretium a sem aliquam, congue porttitor tortor.
    Sed tempor nisl a lorem consequat, id maximus erat aliquet. Sed sagittis porta libero sed condimentum.
    Aliquam finibus lectus nec ante congue rutrum. Curabitur quam quam, accumsan id ultrices ultrices, tempor et tellus.
  </p>
  <p>
   	 생략
  </p>
  <div class="box" id="one">One</div>
</div>
<div class="box" id="two">Two</div>
    <p>
    생략
  </p>
  <p>
    생략
  </p>
      <p>
    생략
  </p>
  <p>
 		생략
  </p>
</body>
</html>
````



4) position3

````html css
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <style>
        .box{
            display: inline-block;
            width: 100px;
            height: 100px;
            background: slateblue;
            color: white;
        }
       #one{
           position: absolute;
           top: 30px;
           left: 30px;
           background-color: cadetblue;
           z-index: 4;/*우선순위를 결정해주는 것, 정수값이 클수록 먼저 보인다*/
       }
       #two{
           position: absolute;
           top: 40px;
           left: 40px;
           background-color:cornflowerblue;
           z-index: 3;
       } 
       #three{
           position: absolute;
           top: 50px;
           left: 50px;
           background-color:orange;
           z-index: 2;
       }
       #four{
           position: absolute;
           top: 60px;
           left: 60px;
           background-color:peachpuff;
           z-index: 1;
       }
    </style>

<body>
    <div class="box" id="one">One</div>
    <div class="box" id="two">Two</div>
    <div class="box" id="three">Three</div>
    <div class="box" id="four">Four</div>
</body>
</html>
````



5) position4

````html css
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <style>
        .box{
            display: inline-block;
            width: 100px;
            height: 100px;
            background: slateblue;
            color: white;
            float: right; /*배치 규칙을 지정 배치*/
        }
        p{
            clear: both; /*이전의 float속성은 다 없앤다, float속성은 계속 유지되니 해지시켜줘야 한다. */
            text-shadow: 
            /*그림자 만들 원본으로부터 떨어진 x좌표(양수:오른쪽, 음수:왼쪽)
            그림자 만들 원본으로부터 떨어진 y좌표(양수: 아래쪽 음수: 위쪽)
            음영이 퍼지는 크기 px
            색상*/
        }
    </style>

<body>
    <div class="box" id="one">One</div>
    <div class="box" id="two">Two</div>
    <div class="box" id="three">Three</div>
    <div class="box" id="four">Four</div>
    <p> 단락입니다 </p>
</body>
</html>
````

