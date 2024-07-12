# XHR(XMLHttpRequest)
    웹 개발에서 자주 사용되는 API 중 하나로, 클라이언트(웹 브라우저)와 서버 간의 데이터를 비동기적으로 교환하기 위해 사용됨 
    여기서 비동기적이라는 것은, 서버로부터 응답을 기다리는 동안 웹 페이지가 멈추지 않고 다른 작업을 계속 수행할 수 있음을 의미
    주로 AJAX 기술과 함께 사용됨

# XHR 주요기능
  1. HTTP 프로토콜을 사용하여 서버에 요청을 보내고 응답을 받음 <br>
     이 요청은 GET, POST, PUT, DELETE와 같은 다양한 HTTP 메서드를 사용가능

  2. 비동기 방식으로 요청을 보내기 때문에, <br>
     서버로부터 응답을 기다리는 동안 웹 페이지에서 사용자가 다른 작업 가능

  3. 요청과 응답 데이터는 XML뿐만 아니라 JSON, HTML, 텍스트 등 다양한 형식으로 주고받을 수 있음

  4. 웹 페이지가 전체를 다시 로드하지 않고도 서버와 데이터를 주고받을 수 있게 해줌 <br>
     예를 들어, 새로운 메시지를 받아오거나 실시간 알림을 표시가능

# XHR과 CGI의 관계성
    XHR과 CGI는 웹 애플리케이션 개발 과정에서 서로 보완적으로 사용가능
    예를 들어, 클라이언트 측에서 XHR을 사용하여 서버에 데이터를 비동기적으로 요청하고, 
    서버 측에서는 CGI를 사용하여 이 요청을 처리하고 데이터를 생성하거나 처리하여 클라이언트에게 응답   

# Chat-gpt를 활용한 XHR 예제코드
```html
// html 파일
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script src="js/my.js" type="text/javascript"></script>
</head>
<body>
	여기는 index.html 입니다. <br>
	
	무엇을 도와드릴까요? <br>
	
    	<input type="text" name="question" id="question">
    	<button onClick="loadDoc()">전송</button>
	
	<hr>
	
	<div id="demo"></div>
</body>
</html>
```

```javascript
// js 파일
// XHR 객체 호출
function loadDoc() {
  var xhr = new XMLHttpRequest(); // XMLHttpRequest 객체 생성
  xhr.onreadystatechange = function() { // 상태 변화 이벤트 핸들러 설정
    if (this.readyState == 4 && this.status == 200) { // 요청 완료 및 응답 상태 확인
      document.getElementById("demo").innerHTML = this.responseText; // 서버에서 받은 응답을 demo 요소에 표시
    }
  };
  var question = document.getElementById("question").value; // 사용자가 입력한 질문 가져오기
  xhr.open("POST", "main", true); // POST 방식으로 main URL에 요청을 준비
  xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded"); // 요청 헤더에 Content-Type 설정 (폼 데이터를 인코딩한 형식)
  xhr.send("question=" + encodeURIComponent(question)); // 질문을 인코딩하여 요청 본문에 포함하여 서버에 전송
}
```
    
``` java
// servlet 파일
package web.controller;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.HttpURLConnection;
import java.net.URL;

import org.json.JSONArray;
import org.json.JSONObject;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

public class MyServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;
    private static String API_KEY = "API 키";
    private static String GPT_URL = "https://api.openai.com/v1/chat/completions";

    public MyServlet() {
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8"); // 한글 처리
        PrintWriter out = response.getWriter(); // PrintWriter를 통해 서블릿이 클라이언트(웹브라우저)로 데이터 전송
        out.println("doGet 호출됨 <br>");

        gpt(request, out);
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8"); // 한글 처리
        PrintWriter out = response.getWriter(); // response 로부터 printerWriter 객체를 가져와 서블릿이 클라이언트(웹브라우저)로 데이터 전송
        out.println("doPost 호출됨 <br>");
        
        gpt(request, out);
    }

    private void gpt(HttpServletRequest request, PrintWriter out) throws IOException {
        URL url = new URL(GPT_URL);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();

        connection.setRequestMethod("POST"); // 메서드 방식 POST 설정
        connection.setRequestProperty("Content-Type", "application/json"); // json 데이터 타입 설정
        connection.setRequestProperty("Authorization", "Bearer " + API_KEY);
        connection.setDoInput(true); // 입력 가능하게 설정
        connection.setDoOutput(true); // 출력 가능하게 설정

        JSONObject data = new JSONObject();
        data.put("model", "gpt-3.5-turbo"); // gpt 모델 설정
        data.put("temperature", 0.7); // 답변 정확도 설정

        JSONObject message = new JSONObject(); // json 객체 생성
        message.put("role", "user");
        message.put("content", request.getParameter("question")); // 질문 내용 작성
        System.out.println(request.getParameter("question"));
        
        JSONArray messages = new JSONArray(); // Json 객체를 담을 배열 생성
        messages.put(message); // 

        data.put("messages", messages);

        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(connection.getOutputStream()));
        bw.write(data.toString()); // data 객체를 문자열로 변환하여 전송
        bw.flush();
        bw.close();

        BufferedReader br = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        StringBuilder sb = new StringBuilder();
        String line;

        while ((line = br.readLine()) != null) {
            sb.append(line);
        }

        br.close();

        // JSON 파싱
        JSONObject jsonResponse = new JSONObject(sb.toString());
        JSONArray choices = jsonResponse.getJSONArray("choices");
        JSONObject firstChoice = choices.getJSONObject(0);
        JSONObject messageResponse = firstChoice.getJSONObject("message");
        String content = messageResponse.getString("content");

        // 출력 예시
        out.println(content);
    }
}
```

![제목 없음](https://github.com/user-attachments/assets/d379bbd6-b8f7-4dbf-942d-a88e9c447b03)
     
	주의 !request.getParameter로 값을 얻어오기 위해서는 xhr에서 요청헤더를 보낼때 반드시 Content-Type을 폼데이터로 보내주어야함
