# application과 session의 차이
application은 모든 브라우저를 공유했다. 반대로 session은 브라우저 별로 값을 따로따로 공유했다.
그런데 session에서 크롬으로 여러창을 띄워서 테스트 했을 때
하나의 창에 입력했던 값을 다른 창에서 받을 수 있었는데 이유는 작업관리자에서 프로세스를 보면
하나의 크롬이 여러 크롬을 쓰레드형식으로 공유하는것을 볼 수 있다. 그래서 크롬끼리는 공유하게 되는 것이다. 다른 브라우저도 마찬가지일 것.

어떻게 이 결과를 도출하게 됬는가? 실험순서는 이렇다.
다른 브라우저가 아닌 크롬 브라우저에서만 새 창 띄워서 실험.
1. 크롬에서 3이란 값을 입력하고 + 를 누른다. // 그럼 3을 저장한 상태가 될 것이다.
2. 다른 크롬창에서 3이란 값을 마찬가지로 입력하고 = 를 누른다 // 바로 6의 값이 나온다!

크롬과 다른 브라우저끼리의 실험.
1. 크롬에서 3값 입력하고 + 를 누른다.
2. 다른 브라우저에서 3을 입력하고 = 를 누른다. 에러가 뜬다.!

이런식으로 session은 해당 브라우저에서만 값이 공유된다.

코드는 아래와 같다.
application을 session으로만 변경해줬다.
```
//		ServletContext application = request.getServletContext();
		HttpSession session = request.getSession(); // servlet > session
    
    //			int x = (Integer)application.getAttribute("value2");
			int x = (Integer)session.getAttribute("value2");
      
      //			String oper = (String)application.getAttribute("operator");
			String oper = (String)session.getAttribute("operator");
      
      //			application.setAttribute("value2", value);
//			application.setAttribute("operator", op);
			session.setAttribute("value2", value);
			session.setAttribute("operator", op);
```

https://www.youtube.com/watch?v=q9nQCnM4NAI&list=PLq8wAnVUcTFVOtENMsujSgtv2TOsMy8zd&index=28 - 9:07 세션에서 타임아웃 하기 위한 다양한 명령어들
