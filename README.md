
# NADO (나의 도시를 찾아서)
### 협업 도구
---
###### Jira , Confluence
https://jiwonkim.atlassian.net/jira/software/projects/CAPSTONE/boards/1
<br>

### 기술 스택
---


#### Back-End
+ Java 11
+ Spring Boot 2.7.11
+ Gradle
+ Spring Data JPA
+ Spring Security
+ linux
+ Postman
+ MySQL 8.0
+ Chat GPT


### Front-End
+ TypeScript
+ React.js

  <br>

### 주요 개발
---
<b>1)	전체 시스템 아키텍쳐 및 프로세스</b>
<br>

![image](https://github.com/capstone-team02/readme/assets/78153919/beb15818-58d5-466b-b114-af98dc6be784)

<br>
&nbsp; 해당 서비스는 실제 웹서비스를 사용하는 <b>‘사용자’</b>, 사용자의 요청을 받아 처리하는 <b>‘시스템’</b>, 데이터 적재를 하는 <b>‘서비스 주체'</b>, 그리고  <b>‘데이터베이스’</b>  네가지  주요  구성 요소로 이루어져 있다.
<br>
<br>
① 회원 시스템은 회원 가입, JWT 를 통한 로그인과 로그아웃, 회원 탈퇴, 회원 수정 프로세스를 수행한다.
<br>
<br>
② 설문조사 시스템은 설문조사 답변 및 chat GPT 를 거친 리뷰 저장, 설문조사 답변 조회, 리뷰 조회의 프로세스가 수행된다.
<br>
<br>
③ 검색 시스템은 동네 테이블을 중심으로 이루어진다. 기본  데이터  적재와  동네별  점수 부여 계산 프로세스가 기본적으로 이루어진 후 메인 페이지에서의 동네 추천, 추천  동네 검색을 위한 조회, 동네별 정보조회 프로세스가 수행된다.
<br>
<br>
④ 챗봇 시스템은 chatGPT 와 채팅 기록 저장, 채팅 기록 조회 프로세스가 수행된다.
<br>
<br>
<br>
  
<b>2) 인터페이스</b>


&nbsp; 서비스의 주요 인터페이스를 다이어그램과 함께 설명한다.


① 설문조사 진행 및 저장


   ![image](https://github.com/capstone-team02/readme/assets/78153919/a2353589-bf10-417b-a2b1-9011541d0cb7)



사용자가 회원가입을 완료하면 해당 정보가 유저 테이블에 저장된다. 이후 설문조사에 답변을 하면 해당 답변은 설문조서 DTO 에 우선적으로 저장된다. 이 저장된 답변들로부터 후처리를 거친 후 chat GPT 에게 리뷰 생성을  요청하고,  응답을  받는다면  해당  리뷰와  함께 설문조사 답변 정보들이 최종적으로 설문조사 테이블에 저장된다.


② open API 데이터와 .csv 파일 데이터 적재


![image](https://github.com/capstone-team02/readme/assets/78153919/d1361b9e-eb5d-412b-992c-238d076482a8)


데이터 적재 요청을 하면 미리 준비된 .csv 파일로부터 구, 동, 인구정보, 시설정보 테이블에 데이터가 적재된다. 이후 open API 링크를 통해 부동산 정보가 부동산 테이블에 적재된다.

③ 동네별 순위 부여

![image](https://github.com/capstone-team02/readme/assets/78153919/086eacd5-8045-448c-8b7c-42b104ec38c7)


동네별 순위 계산 요청으로부터 동네의 인구 수 및 밀집도 데이터와  시설의  데이터에 따라 score 테이블에 동네별로 저장이 된다.


 ④ 동네 검색 결과

![image](https://github.com/capstone-team02/readme/assets/78153919/7832345a-80a1-4c25-8f82-82a2675e17da)


Client 단에서 사용자는 원하는 조건을 선택한 후 동네를 검색한다. 해당 조건을 바탕으로   동 테이블에서 조건에 적합한 동네를 찾고 해당 동네는 검색 결과로 보인다. 결과 창에서 동네의 핵심 키워드, 장단점, 리뷰와 부동산 정보를 보여주기 위해 결과에 해당하는 동네의 정보를 조회하여 다시 Client 로 응답을 보낸다.
