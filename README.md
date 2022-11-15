# vaccine
# 백신 예약 프로그램 만들기
# 환경 셋팅
### 1. 오라클, jdk1.8, 톰캣을 다운로드한다.
### 2. jdk1.8버전을 확인하기 위해서 cmd 창에서 javac를 입력하여 확인한다.
### 3. 제어판 - 시스템- 고급 시스템 설정- 환경변수에 들어가 path 클릭 후 편집에 들어가 새로 만들기를 누른 후 '%JAVA_HOME%'을 추가 하고 시스템 변수를 새로 만들기 하여 변수 이름을 JAVA_HOME 변수 값을 JDK 설치 디렉토리\BIN으로 설정한다.
### 4. 오라클 설치 후 패스워드를 1234로 지정한 후 cmd 창에서 sqlplus를 이용하여 접속을 확인한다.
### 5. 오라클 확인 후 바탕화면에 새로운 폴더를 만들어 이클립스 workspace로 지정한다.
### 6. 이클립스 실행 후 프로젝트에 톰캣 8.5를 연결 시킵니다. 이때 톰캣 권장 포트는 8090,8005,1023,1000이 있습니다.
### 7. 프로젝트 내에서 DB를 연결합니다. 연결 할 때 오라클은 oracle thindriver  oracle 11로 설정하고 ojdbc14.jar 삭제하고  ojdbc6.jar 추가합니다. 또 service Name은 xe로 설정하고 host는 localhost, user name은 system, password는 1234로 확인합니다.
# jsp페이지
### webapp 아래 layoyt 폴더를 만든 후 폴더 안에 header,nav,section,footer 4개의 jsp를 만들고, webapp 아래 index,reservatoin,reservatoin_p,member_list,search,search_p,total 7개의 jsp 페이지를 만든다. 또 DBConnect.java라는 데이터베이스 연결 페이지를 만들어준다.(style.css페이지는 필수 사항이 아니지만 css로 꾸미고 싶은 사람은 사용한다.)
# DB분석
### 데이터베이스에서 테이블은 TBL_JUMIN_202108, TBL_HOSP_202108, TBL_VACCRESV_202108 3개의 테이블생성한다. 폼안에 입력양식들의 name 속성은 오라클 쿼리문에 테이블 컬럼명과 동일하게 작용한다.
# 실행 화면 (reservation.jsp)
![1](https://user-images.githubusercontent.com/104752580/201795452-95412c99-05c8-4922-b7ab-0124461dd084.PNG)
![2](https://user-images.githubusercontent.com/104752580/201795455-b5a75f87-0e33-42c2-8975-54d75ce90b79.PNG)
# 실행 코드 설명 (reservation.jsp)
```jsp
<%@ page import="DB.DBConnect" %>
<%@ page import="java.sql.*" %>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
String sql = "select max(RESVNO) from TBL_VACCRESV_202108";

Connection conn = DBConnect.getConnection();
PreparedStatement pstmt = conn.prepareStatement(sql);
ResultSet rs = pstmt.executeQuery();

rs.next();
int num = rs.getInt(1)+1;

%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<link rel = "stylesheet" type= "text/css" href="css/style.css?abc">
<title>Insert title here</title>
<script type="text/javascript">
function checkValue(){
	if(!document.data.RESVNO.value){
		alert("예약번호가 입력되지 않았습니다.");
		data.RESVNO.focus();
		return false;
	}else if(!document.data.JUMIN.value){
		alert("주민번호가 입력되지 않았습니다.");
		data.JUMIN.focus();
		return false;
	}
	else if(!document.data.VCODE.value){
		alert("백신코드가 입력되지 않았습니다.");
		return false;
	}
	else if(!document.data.HOSPCODE.value){
		alert("병원코드가 입력되지 않았습니다.");
		return false;
	}
	else if(!document.data.RESVDATE.value){
		alert("예약날짜가 입력되지 않았습니다.");
		data.RESVDATE.focus();
		return false;
	}
	else if(!document.data.RESVTIME.value){
		alert("예약시간이 입력되지 않았습니다.");
		data.RESVTIME.focus();
		return false;
	}
	return true;
}	
</script>
</head>
<body>
<header>
<jsp:include page="layout/header.jsp"></jsp:include>
</header>
<nav>
<jsp:include page="layout/nav.jsp"></jsp:include>
</nav>
 <section class = "section">
<h2>백신예약</h2>
<form name="data" method="post" action="reservation_p.jsp" onsubmit="return checkValue()">
<table class="table_line">
<tr>
<th>예약번호</th>
<td><input type="text" name="RESVNO" value="<%=num%>" readonly></td>
</tr>
<tr> 
<th>주민번호</th>
<td><input type="text" name="JUMIN"></td>
</tr>
<tr>
<th>백신코드</th>
<td>
<select name="VCODE">
<option value="V001">A백신</option>
<option value="V002">B백신</option>
<option value="V003">C백신</option>
</select>
</td>
</tr>
<tr>
<th>병원코드</th>
<td>
<label><input type="radio" name="HOSPCODE" value="H001">가_병원</label>
<label><input type="radio" name="HOSPCODE" value="H002">나_병원</label>
<label><input type="radio" name="HOSPCODE" value="H003">다_병원</label>
<label><input type="radio" name="HOSPCODE" value="H004">라_병원</label>
</td>
</tr>
<tr>
<th>병원코드</th>
<td>
<label><input type="checkbox" name="HOSPCODE" value="H001">가_병원</label>
<label><input type="checkbox" name="HOSPCODE" value="H002">나_병원</label>
<label><input type="checkbox" name="HOSPCODE" value="H003">다_병원</label>
<label><input type="checkbox" name="HOSPCODE" value="H004">라_병원</label>
</td>
</tr>
<tr>
<th>예약날짜</th>
<td><input type="text" name="RESVDATE"> </td>
</tr>
<tr>
<th>예약시간</th>
<td><input type="text" name="RESVTIME"> </td>
</tr>
<tr>
<th colspan="2">
<input type="submit" value="등록">
<input type="reset" value="취소">
</th>
</tr>
</table>
</form>
</section>
 <footer>
<jsp:include page="layout/footer.jsp"></jsp:include>
</footer>	
</body>
</html>



```
### 1. DB.DBConnect와 java.sql.*을 이용하여 DB와 sql을 연결합니다.
### 2. 예약번호를 자동완성을 시키기 위해서 백신 테이블에서 마지막 예약번호를 받아오는 쿼리문을 작성합니다.
### 3. 마지막 예약 번호를 받아온 후에 nun 값에 마지막 번호에서 +1를 더한 값을 넣어줍니다.
### 4. 테이블 생성 후 각 행마다 name을 지정해 줍니다.
### 5. 예약 번호 행에는 value 값을 num으로 자동완성 해주고 readonly 속성을 사용하여 읽기전용으로 바꿔줍니다.
### 6. 마지막 행에는 등록과 취소라는 버튼을 만들고 등록을 누르게 되면 reservation_p.jsp로 페이지가 넘어가게 name 속성을 submit으로 지정합니다. 취소에 name 속성은 reset을 사용하여 테이블 내용을 초기화 시켜줍니다.
### 7. 폼 태그로 테이블을 감싸면서 테이블의 유효성 검사와 reservation_p.jsp 페이지로 이동을 위한 onsubmit을 시켜줍니다. 
### 8. 유효성 검사를 위해서 head 태그 안에 스크립트 문을 작성합니다. 스크립트 안에서 checkValue 함수를 지정하고 테이블 행에 갑을 입력하지 않고 등록을 눌렀을 경우에 값을 입력하라는 문구가 나오는 코드를 작성합니다. 마지막으로 테이블에 내용을 알맞게 입력하고 등록을 누르면 reservation_p.jsp 페이지로 이동하는 값을 반환합니다.
