---
title: "프로젝트 JPP-Bank"
date: 2025-08-11 18:00:00 +0900
categories: [Project, FrontEnd]
tags: [Spring boot, JavaFx, MySQL]
image:
    path: /assets/img/JPPBANK-logo.png
---

## 📋 Overview

| 항목 | 내용 |
| :--- | :--- |
| 👤 **Role** | `FE` |
| 🔗 **Link** | [&nbsp;FE 바로가기](https://github.com/Rainier102625/KDT_BANK)&nbsp;&nbsp;&nbsp;&nbsp;[BE 바로가기](https://github.com/Rainier102625/KDT_BANK_SERVER) |
| ⏱️ **기간** | 2025.07.28 ~ 2025.08.11 |
| 🖋️ **Stack** | `Spring Boot` `JavaFx` `MySQL` |

## 1. 개요

### 주제에 맞는 프로그램 만들기

* 회사, 은행, 병원 중에 한가지 주제 선정  
* 주제를 토대로 JavaFX를 통한 사내 윈도우 프로그램 만들기  
* 선정한 것 = 은행
* 프로그램: 사내 창구 업무 프로그램  

#### ➡️ 은행 사내 업무를 위한 프로그램:JPP-Bank 결정

## 2. 주요 기능

* 은행 고객의 신상정보 관리
* 은행 고객 신청 상품의 승인,허가를 관리
* admin 권한을 가진 직원의 사내 직원 관리
* 사내 메신저 구현
* 새로운 데이터 생성 및 기존 데이터 수정 시 전직원에게 알람(강사님 피드백)

## 3. 플로우 차트

<div style = "text-align: center">
    <img src ="/assets/img/posts/JPPBank/JPPBankFlowChart.png" alt ="JPPBankFlowChart" width="100%" height="auto">
</div>
<br>

&nbsp;
우리는 로그인 세션, 회원가입을 상정하고 관리자인가 아닌가에 따라 추가기능이 설정되는 형식이다. 이 프로그램에 가입한 인원은 사내 직원 페이지 목록이 뜨지 않으며 기본적인 창구 기능만 할 수 있다.

## 4. 기술  

### 4.1 스택  

* FE: JavaFX
* BE: Spring Boot
* DB: MySQL

### 4.2 기능 맵

```html
KDT_BANK  
├── 인증  
│   ├── 로그인 (loginController)  
│   └── 회원가입 (SignupController)  
├── 메인 대시보드 (MainViewController)  
│   └── 알림 시스템 (실시간 WebSocket + REST)  
├── 공지사항  
│   ├── 목록 조회 + 페이지네이션   (NoticeViewController)  
│   └── 상세/생성/수정/삭제 (NoticeDetailController)  
├── 채팅 (ChatViewController)  
│   ├── 실시간 메시지 (STOMP WebSocket)  
│   ├── 채팅방 생성 (createChatController)  
│   ├── 친구 추가 (friendaddController)  
│   └── 채팅방 초대 (friendinviteController)  
├── 고객 관리 (관리자)  
│   ├── 고객 검색 (CustomerSearchController)  
│   └── 고객 상세 조회 (CustomerCheckController)  
├── 직원 관리 (관리자)  
│   ├── 직원 목록/삭제 (EmployeeCheckController)  
│   └── 직원 정보 수정 (EmployeeEditController)  
├── 상품 관리 (관리자)  
│   ├── 상품 목록/삭제 (ProductManagementController)  
│   └── 상품 추가 (ProductaddController)  
├── 계좌 승인 (관리자) (AccountapprovalController)  
└── 마이페이지 (mypageController)  
```

### 4.3 기여한 부분

#### 로그인 (loginController)

* JWT 기반 인증, 로그인 성공 시 tokenManager, UserSession에 저장
* 로그인 후 WebSocket 연결 (WebSocketManager.connect()) 자동 수행
* WebSocket 연결 완료 후 MainView로 전환

#### 회원가입 (SignupController)

* 이름/ID/비밀번호/전화번호/생년월일/부서/직급 입력 후 가입

#### 알림 시스템 (MainViewController)

* 로그인 후 /topic/notify/{userIndex} WebSocket 구독
* 새 알림 수신 시 종 아이콘 깜빡임 애니메이션 + 뱃지 숫자 갱신
* 종 클릭 → NotificationPanel 팝업으로 전체 알림 목록 확인
* 알림 읽음 처리: POST /notifications/mark-read

#### 공지사항(NoticeViewController)

* 전체 공지사항 조회 후 페이지당 10개씩 표시
* 페이지네이션 버튼 동적 생성
* 공지사항 클릭 -> 상세 팝업
* 관리자만 "생성"버튼 노출

#### 공지사항 CRUD(NoticeDetailController)

* 관리자: 수정/삭제 메뉴 버튼 노출
* 수정 시 제목/내용 TextField를 편집 가능 상태로 전환

#### 채팅 (ChatViewController)

* 왼쪽: 친구 목록 / 채팅방 목록 탭 전환
* 채팅방 클릭 → 과거 메시지 로드 + WebSocket /topic/chat/{chatIndex} 구독
* 메시지: 내 메시지(우측), 상대방 메시지(좌측) 정렬
* 우측 패널: 현재 채팅방 참여자 목록 (이름/부서/직급)
* 채팅방 나가기, 친구 초대 기능

## 5. 결과물

### 5.1 요약

<table id = "post-table">
  <tr>
    <th>로그인화면</th>
    <th>회원가입</th>
  </tr>
  <tr>
    <td>
        <img src = "/assets/img/posts/JPPBank/projectImage/JPP_Login.png " alt="로그인화면">
    </td>
    <td >
      <img src = "/assets/img/posts/JPPBank/projectImage/JPP_SignUp.png" alt="회원가입">
    </td>
  </tr>
  <tr>
    <th></th>
    <th></th>
  </tr>
  <tr>
    <th>메인페이지(공지사항)</th>
    <th>공지사항 생성</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Notice.png " alt="메인화면">
    </td>
    <td >
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Notice_Create.png" alt="공지사항 만들기">
    </td>
  </tr>
  <tr>
    <th>공지사항 수정</th>
    <th>상품 관리 페이지</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Notice_Update.png " alt="공지사항 수정">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Products.png" alt="상품 관리 페이지">
    </td>
  </tr>
  <tr>
    <th>상품 추가 페이지</th>
    <th>고객 조회 페이지</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Product_Add.png " alt="상품 추가">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Client.png" alt="고객 조회">
    </td>
  </tr>
  <tr>
    <th>고객 상세정보 페이지</th>
    <th>마이페이지</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Client_Detail.png" alt="고객 상세조회">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_MyPage.png" alt="마이페이지">
    </td>
  </tr>
  <tr>
    <th>채팅-메인</th>
    <th>채팅-목록</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Chat_Main.png " alt="채팅방 메인">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Chat_Friend.png" alt="채팅 친구 목록">
    </td>
  </tr>
  <tr>
    <th>채팅-참여</th>
    <th>채팅-초대</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Chat.png " alt="채팅 참여 목록 및 채팅방">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Chat_Invite.png" alt="채팅방 초대 페이지">
    </td>
  </tr>
  <tr>
    <th>사원 조회</th>
    <th>사원정보 수정</th>
  </tr>
  <tr>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Staff.png " alt="사원 조회 페이지">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Staff_Update.png" alt="사원정보 수정 페이지">
    </td>
  </tr>
  <tr>
    <th>계좌개설</th>
    <th>알림</th>
  </tr>
  <tr>
    <td>
      <img src="assets\img\posts\JPPBank\projectImage\JPP_Product_Confirm.png" alt="계좌개설 승인 페이지">
    </td>
    <td>
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Alarm.png" alt="알림 팝업">
    </td>
  </tr>
</table>
