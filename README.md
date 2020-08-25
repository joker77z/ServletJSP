# ServletJSP
SERVLET과 JSP의 설명 : https://m.blog.naver.com/acornedu/221128616501
TOMCAT 설명 : https://namu.wiki/w/%ED%86%B0%EC%BA%A3

1. tomcat 9버전 설치  
2. 설치한 경로 들어가서 bin - startup.bat 을 실행시켜서 tomcat창에 문구가 쫙 나오고 cmd창이 안꺼지면 잘 실행 된 것.  
3. localhost:8080 or localhost:8080/index.jsp 로 접속하면 메인 창이 뜬다. (창이 뜨면 잘 접속된 것.)  
4. test용으로 tomcat 설치한 폴더에 webapps - ROOT 로 들어가서 nana.txt를 만들고 내용은 아무렇게나 쓴 뒤 저장 한다. 
(같은 공유기를 쓰고 있는 핸드폰이 있다면 ipconfig로 ipv4의 ip를 확인해서 192.168.0.15:8080/nana.txt 쓰면 똑같이 확인 가능하다.)  

* Context  
작업을 협엽하다보면 webapps > ROOT 여기안에서 여러 폴더로 분산하는 것은 정신없기 때문에  
따로 다른 곳에 장소를 마련해야 한다. 여기서는 예를 들어서 webapps > ITROOT 라는 폴더를 만들고 안에 news.txt라는 것을 넣겠따.  
다음 conf 폴더로 이동해서 server.xml 원본파일을 복사해서 복사본으로 만들어서 그대로 두고 server.xml 파일을 수정하는데  
아래와 같이 host 부분 밑에 Context로 추가해준다.  
그런데 이 방법은 사용하게 되면 서버를 껏다켜야된다. 그래서 이 방법말고 다른데에서 메타파일로 만들 수 있는데 그건 나중에 알아보자  

      <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
	<Context path="it" 
	docBase="C:\Users\CAD support depart\Downloads\apache-	tomcat-9.0.37-windows-x64\apache-tomcat-9.0.37\webapps	\ITWEB" 
	privileged="true"/> 

5. 바탕화면에 jsp 폴더 만들고 nana.java 를 만든다. 내용은 아래와 같다.  

/

	import javax.servlet.*;
	import javax.servlet.http.*;
	import java.io.*;
	
	public class nana extends HttpServlet
	{
		public void service (HttpServletRequest request
				, HttpServletResponse response)
				throws IOException, ServletException
		{
			System.out.println("hello Servlet");
		}
	}
	

그 다음에 cmd에서 cd [경로] 를 이용해서 바탕화면에 jsp 폴더내로 이동하고  
     javac       -cp   -cp "C:\Users\CAD support depart\Downloads\apache-tomcat-9.0.37-windows-x64\apache-tomcat-9.0.37\lib\servlet-api.jar" nana.java  
(자바컴파일러)  (api를 불러올 경로)                                          								    (파일이름)
  
6. dir을 쳐보면 nana.class 파일이 생성된 것을 알 수 있다.  
  
예행연습을 끝냈으니 제대로 시작할 시간  
1. apache-tomcat-9.0.37\webapps\ROOT\WEB-INF 에 classes라는 폴더를 만들고 그 폴더안에 nana.class 파일을 넣는다.  
2. 그 다음 web.xml 파일을 수정하는데 아래와 같이 입력해 넣는다.


/

	<servlet>
		<servlet-name>na</servlet-name>
		<servlet-class>nana</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>na</servlet-name>
		<url-pattern>/hello</url-pattern>
	</servlet-mapping>
	~~Welcome to Tomcat~~
  
3. 인터넷 주소에 http://localhost:8080/hello 라고 입력하면 nana.class 파일을 읽어온다.  
(이 때 빈 공백화면이 뜨면 정상이고 tomcat cmd창을 보면 hello Servlet 문구가 나오는 것을 볼 수 있는데 우리가 서버 콘솔쪽으로 메시지를 보냈기 떄문이다.)  
  
4. 이제 클라이언트(웹)쪽에 글자를 송출해보자.  
5. classes 폴더 안에 있는 nana.java 파일을 오픈하고 아래 코드를 입력한다.  

		OutputStream os = response.getOutputStream();
		PrintStream out = new PrintStream(os, true);
		out.println("Hello Servlet!!");

6. 다시 java -> class 파일로 되게 컴파일한다.(아직 이클립스 사용전이라는 가정하에 불편하게 하는 것)  
7. tomcat이 다시 읽을 수 있게 tomcat 껐다가 startup.bat 다시 킨다.  
8. http://localhost:8080/hello 다시 접속했더니 문구가 나온다.  

* nana.java에 입력했던 문구를 수정할 수도 있다. PrintStream을 사용하는 것이 아니라 PrintWriter를 사용하는 방법.
PrintWriter out = response.getWriter();
out.println("Hello Servlet");

PrintWriter는 다국어를 지원한다. 우리는 한국어라서 Writer를 써도 된다.

  

## 이클립스를 함께 사용해서 개발진행
https://www.youtube.com/watch?v=b_YnVlJmZ7Q&list=PLq8wAnVUcTFVOtENMsujSgtv2TOsMy8zd&index=10

1. enterprise 용 이클립스 설치  
2. JSPprj 라는 프로젝트를 만든다.  
3. Webcontent가 기본 루트인데 index.html 을 만들고 실행을 해보니까 루트명에 JSPprj가 들어가있다. 이걸 빼기 위해서 프로젝트 - 우클릭 - 프로퍼티 들어가서 [Web Project Settings]에서 Context root에 /를 입력해준다.  
4. 그리고나서 서버를 중지시키고 [Servers] 하위에 있는 JSPprj를 삭제한뒤 다시 CTRL+F11 해준다.  
5. URL이 ------/index.html 만 나오는 것을 확인할 수 있다.  
6. 그 다음 java소스는 Java Resources > src에 만들 것이다.  
7. 여기서 nana 클래스 파일을 작성하면서 package 개념을 같이 공부하기 위해 com.parktaejoon.web 을 써주자.  
8. 다음 nana extends 다음 http정도 쓰고나서 ctrl+space누르면 자동완성으로 추천해주는데 HttpServlet 이 나오도록 하자. 

```
public class nana extends HttpServlet{
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		PrintWriter out = resp.getWriter();
		out.println("hello");
	}
}
```

9. nana라는 서블릿 클래스를 매핑해야 한다. (주소창에 hello 쳐도 nana라는 창이 나오게)  
10. web.xml 파일을 WebContent > WEB-INF 안에 넣고 더블클릭해서 수정으로 들어가서 아래와 같이 바꿔준다.
```
	<servlet>
		<servlet-name>na</servlet-name>
		<servlet-class>com.parktaejoon.web.nana</servlet-class>
	</servlet>

	<servlet-mapping>
		<servlet-name>na</servlet-name>
		<url-pattern>/hello</url-pattern>
	</servlet-mapping>
```

11. 하지만! 이렇게 할 필요 없다. 간편해졌다. 서블릿 3.0으로 오면서!  
12. web.xml에서 metadata-complete="true"로 되어있는걸 false로 설정해주고 서블릿, 서블릿 매핑 내용을 지워준다.  
13. 다음 아래와 같이 어노테이션을 추가해준다.
```
@WebServlet("/hi")
public class nana extends HttpServlet{
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		PrintWriter out = resp.getWriter();
		out.println("hello");
	}
}
```
