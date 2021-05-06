# File읽고 쓰기 

> 데이터 분석에 최적화될 수 있도록, 분석화에 맞는 데이터를 찾아내기 위해 이전 전처리작업이 들어가야 한다. 가령 필요한 데이터 형태가 비어있거나, 정수타입이 문자열로 나와있을 수 있다. 그런 것들은 분석에 최적화된 것이 아니다. 이것을 덜어내기 위한 전처리작업이 필요한 것. 
>
> 파이썬은 데이터소스로부터 데이터를 가져와서 분석된 결과물을 남겨야 한다. 파일을 열고, 읽고, 쓰고, 닫는(open, read, write, close)과정이 필요하고 테이블형태나, 그래프 형태로 남기기도 함.



* 파일 읽고 쓰고 진행되는 곳은 현재 파일 작성 디렉토리에서 진행 (경로 조회)

* 파일 읽기 (read)

  **open** - 파일을 읽거나 수정하거나 가장 필수적으로 먼저 open을 사용해야 한다 

  open('파일명', 'r|w|a')

  * read=r | write=w | append=a 
  * read
  * r의 경우 text로 읽어옴 
    * rt는 원래파일
    * rb는 png이미지파일 
  
  ````python
  #파일 읽기
  import os
  print(os.getcwd())
  print(os.listdir())
  #['a.py', 'modultest.py', 'filetest.py', 'second.py', 'exceptiontest.py']
  try:
        file = open('modultest.py', 'r')#read=r | write=r | append=a 
        print(file.read()) #str
  except FileNotFoundError:
        print('파일 없음')
  file.close()
  
  ````



* 파일 추가하기 

  * wirte

    * 해당 파일이 없다면 새로운 파일을 생성 후 변수값을 작성 
    * 해당 파일이 있다면, 기존에 있던 내용 사라지고 추가한 내용값 생성 

    ````python
    file2 = open('a.txt', 'w')
    file2.write('파일 없으면 새로운 파일을 생성')
    file2.close()
    ````

  * append

    * 해당 파일이 없다면 새로 생성 후 변수값 작성
    * 해당 파일이 있다면, 기존 내용 뒤에 값 추가 

    ````python
    file2=open('a.txt', 'a')#파일 없으면 새로 생성/ 파일 있으면 기존 내용 뒤에 추가 쓰기 저장
    file2.write('\n새로운 라인을 추가')
    file2.close()
    ````



* 파일 활용하기(예제)

  ````python
  #파일 한 라인씩 읽어서 리스트에 저장
  
  file_list = [] # ==file_list=list()
  file3 = open('modultest.py', 'r')
  #1
  
  for line in file3:
        file_list.append( line)
  file3.close()
  
  
  i = 1
  for line in file_list:
        print(i, '번:', line, end=" ")#숫자 추가해서 출력
        i = i +1
  
  #print default: print(*val, seq=' ', end='\n')
  
  #2
  for index in range(0, len(file_list), 1):
        print(index+1, '번:', file_list[index], end=" ")#숫자 추가해서 출력
        
  #라인번호 있는 상태의 모든 내용을 파일copy.txt에 저장
  file4 = open("copy.txt", "w") #없을시 새로 생성
  for index in range(0, len(file_list), 1):
        file4.write(str(index+1)+ '번:'+ file_list[index])
  file4.close() #반드시 닫아주기
  ````






#### raspberrypi에서 spring server로 file 전송하기

> Spring에 FileUpload가 구현되어 있는 상태 가정



1. Spring이 깔려있는 컴퓨터의 ip주소 알아오기
   * 명령어 ifconfig|grep inet



2. Spring Project tomcat 실행 후 라즈베리파이에서 해당 ip주소 열리는지 확인 



3. 파일 처리 

   ````python
   # 기가지니 호출 정보 데이터 생성
   
   
   def result_test(keyword, rc):
   	global filename
   	#when call test() - time, keword, code -> save to file(result.txt)
   	#setting current time
   	import datetime
   	now = datetime.datetime.now()
   	now = now.strftime("%y-%m-%d %H:%M:%S")
   	#write to file
   	file = open('result.txt', 'a')
   	filename= "result.txt"
   	file.write(now+","+keyword+","+str(rc)+"\n")
   	file.close()
   
   # 데이터 읽어오기
   	# 1. 테이블 형태 출력
     # 2. '기가지니' 호출 횟수/ 코드 200번 생성 횟수 구하기 / 오늘 호출 횟수 구하기 
   def result_read_test():
   	#read result.txt - return stringtype
   	file = open('result.txt', 'r')
   
   	time_list = []	
   	keyword_list = []
   	response_list = []
   	file_dict = {}
   	
   	for line in file: 
   		line_list = line.rstrip().split(',')
   		time_list.append(line_list[0])
   		keyword_list.append(line_list[1])
   		response_list.append(line_list[2])
   
   	file_dict['time'] = time_list
   	file_dict['keyword'] = keyword_list
   	file_dict['response'] = response_list
   
   	file.close()
      
   	for i in file_dict.keys():
   		print(i, end=" ") #end default value=\n
   	print()
   
   	for i in range(0, len(file_dict['keyword']), 1):
   		for k in file_dict.keys():
   			print(file_dict[k][i], end = ' ')
   		print()
   	print(file_dict['keyword'].count('기가지니'))
   	print(file_dict['response'].count('200'))
   
   	#todays call
   	import datetime
   	now = datetime.datetime.now()
   	now = now.strftime("%y-%m-%d")
   
   	today_call = 0 
   	for t in file_dict['time']: 
   		if t[:8] == now:
   			today_call += 1
   	print('today call = ', today_call)
   	return file_dict
   ````

   ````python
   # 그래프 생성/저장하기 
   def result_graph_test():
   	global filename2
   	file_dict = result_read_test()
   
   	#each keyword's call times graph
   	import matplotlib.pyplot as plt
    	import matplotlib.font_manager as fm
   	for f in fm.fontManager.ttflist:
   		print(f.name)
   	plt.rcParams['font.family'] = 'NanumGothic'
   	plt.hist(file_dict['keyword'])
   	plt.title('keyword call count')
   	plt.xlabel('keyword')
   	plt.savefig('key.pdf')
   	filename2 = 'key.pdf'
   	plt.show()
   
   	#show response values with plot(barh)
   	response_cnt_dict = {}
   	for k in set(file_dict['response']):
   		response_cnt_dict[k] = file_dict['response'].count(k)
   	
   	k_list=[]
   	v_list=[]
   	for k, v in response_cnt_dict.items():
   			k_list.append(k)
   			v_list.append(v)
   
   	print(k_list)
   	print(v_list)
   	plt.barh(k_list, v_list)
   	plt.rcParams['font.family'] = 'NanumGothic'
   	plt.title('response count')
   	plt.ylabel('response code')
   	plt.xlabel('response code count')
   	plt.show()
   ````

   ````python
   #전송하기 
   def result_server_test():
   	#전송할 url : http://192.168.0.150:9091/fileupload
   	#result.txt, response.png upload
   	#terminal pip3 install requests
   	import requests as rq
   	textfile = open(filename, 'r')
   	graphfile = open(filename2, 'rb')
   	response = rq.post('http://192.168.0.150:9091/fileupload', 
   						data={'name':'raspberrypi', 'description':'upload test'}, 
   						files={'file1':textfile, 'file2':graphfile})
   	print(response.status_code)
   	print(response.text)
   ````

   

