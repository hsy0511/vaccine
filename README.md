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
### webapp 아래 layoyt 폴더를 만든 후 폴더 안에 header,nav,section,footer 4개의 jsp를 만들고, webapp 아래 index,reservatoin,reservatoin_p,member_list,search,search_p,total 7개의 jsp 페이지를 만든다.
# DB분석
### 데이터베이스에서 테이블은 TBL_JUMIN_202108, TBL_HOSP_202108, TBL_VACCRESV_202108 3개의 테이블을 오라클에서 실행 후 폼화면에서 작동하게 한다(?)
