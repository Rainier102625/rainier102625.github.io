---
title: "프로젝트 GilBot"
date: 2025-11-03 19:43:22 +0900
categories: [Project, FrontEnd, BankEnd]
tags: [Spring boot, Next.js, MySQL, LGBM, Flask]
image:
    path: /assets/img/JPPBANK-logo.png
---

## 📋 Overview

| 항목 | 내용 |
| :--- | :--- |
| 👤 **Role** | `FE` `BE` |
| 🔗 **Link** | [&nbsp;FE 바로가기](https://github.com/Rainier102625/PP_Front)&nbsp;&nbsp;&nbsp;&nbsp;[BE 바로가기](https://github.com/Rainier102625/PP)&nbsp;&nbsp;&nbsp;&nbsp;[Pyhon BE 바로가기](https://github.com/Rainier102625/PP_algorithm) |
| ⏱️ **기간** | 2025.09.28 ~ 2025.11.01 |
| 🖋️ **Stack** | `Spring Boot` `Next.js` `MySQL` `Flask` |

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

## 4. 구현

### 4.1 요약

<table>
  <tr>
    <th style="text-align:center;">로그인화면</th>
    <th style="text-align:center;">회원가입</th>
  </tr>
  <tr>
    <td style="text-align:center;">
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Login.png " alt="로그인화면" width=350px>
    </td>
    <td style="text-align:center;">
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_SignUp.png" alt="회원가입" width=280px>
    </td>
  </tr>
  <tr>
    <th style="text-align:center;">공지사항</th>
    <th style="text-align:center;">공지사항 생성</th>
  </tr>
  <tr>
    <td style="text-align:center;">
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Notice.png " alt="로그인화면" width=350px>
    </td>
    <td style="text-align:center;">
      <img src="/assets/img/posts/JPPBank/projectImage/JPP_Notice_Create.png" alt="회원가입" width=280px>
    </td>
  </tr>

</table>
