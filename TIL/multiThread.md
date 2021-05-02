# multi thread

> process : cpu가 현재 실행 중인 프로그램

> thread : 프로세스를 구성하는 작업단위 

프로세스 내에서 스레드를 실행하는 방식

1. SingleThread : 한 번에 한 번 스레드를 실행 (ex. 플레이 종료 > 뉴스 종료 > 다운로드)
2. MultiThread : 동시 실행 



![스크린샷 2021-03-17 오후 10.56.43](/Users/lulala/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-17%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.56.43.png)

* 자바의 멀티스레드 구현 방법: 

  * java.lang.Thread 클래스

  ```java
  class A extends Thread {
  public void run(){ 
    //overriding
  }
  } 
  
  public static void main(String[] args) {
    A a1 = new A();
  Thread a1 = new A();
    //멀티스레드 객체 생성
    
    a1.start();
    //실행
  }
  ```

  | run()     | overriding           |
  | --------- | -------------------- |
  | start()   | 호출, run 시작       |
  | setName() | 멀티스레드 이름 설정 |
  | getName() | 멀티스레드 이름 조회 |

  

  * java.lang.Runnable 인터페이스

  ```java
  //멀티스레드 클래스 정의 
  class B extends C implements Runnable{
  //C 클래스 상속
  //Runnable 상속  ## 오버라이딩 의무화  
  
  public void run(){ 
    // overriding
     }
    }
  
  public static void main(String[] args) {
   //멀티스레드 객체 생성
   Runnable b1 = new B();
   Thread tb = new Thread(b1); 
    
  //멀티스레드 메소드 실행
  tb.start(); 
  
  }
  ```

  ![스크린샷 2021-03-17 오후 11.03.39](/Users/lulala/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-17%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.03.39.png)

![스크린샷 2021-03-17 오후 11.04.13](/Users/lulala/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-17%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2011.04.13.png)



````java
setPriority(); // - > 1-10사이의 값을 줄 수 있음
setPriority(Thread.MAX_PROIRITY =); // =setPriority(10);  (최대 우선순위)

setPriority(Thread.MIN_PROIRITY =); // 1 
setPriority(Thread.NORM_PROIRITY =); // 기본값 5

getPriority(); 
````



### synchronized

- 2개 이상의 멀티스레드가 동시에 한 개의 객체를 공유하는 작업 환경에 있다면, 여기에서 공유하는 객체를 보호할 필요가 있다. 
- **LOCK** 번에 한 개의 스레드만 접근이 가능하도록 

 ````java
package day6;
//동시실행 내용 생기면 멀티스레드 코드 작성
//동시 실행주에 특정 객체 접근시 synchronized 블록 순서 지키고 1번에 1개 스레드 접근 
class MyStack{
	char[] ch = new char[10];
	int idx = 0;
	void push(char c) {
	    synchronized(ch) {//lock 해
	    	
		ch[idx] = c;
		System.out.println
		(Thread.currentThread().getName()+"idx=" + idx + ", ch[idx]=" + ch[idx]);
		idx++;
		}//lock 설정 
		
	}
}
class MyStackThread extends Thread{
	MyStack st;
	char c; 
	MyStackThread(MyStack st, char c){
		this.st = st;
		this.c = c;
	}
	public void run() {
		for(int i = 1; i <=5; i++) {
			st.push(c);
		}
	}
}
public class SynchronizedTest {

	public static void main(String[] args) {
		MyStack st = new MyStack();
		MyStackThread t1 = new MyStackThread(st, 'a');
		MyStackThread t2 = new MyStackThread(st, 'b');
		t1.setName("t1");
		t2.setName("t2");
		t1.start();
		t2.start();
	}

}
 ````

