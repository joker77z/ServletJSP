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

</

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
/>

그 다음에 cmd에서 cd [경로] 를 이용해서 바탕화면에 jsp 폴더내로 이동하고  
     javac       -cp   -cp "C:\Users\CAD support depart\Downloads\apache-tomcat-9.0.37-windows-x64\apache-tomcat-9.0.37\lib\servlet-api.jar" nana.java  
(자바컴파일러)  (api를 불러올 경로)                                          								    (파일이름)
