---
layout: post
title:  "code snippet test"
date:   2018-07-27
desc: ""
keywords: ""
categories: []
tags: []
icon: icon-html
---

## 스마트택배

### 기간
2016.02 ~ 현재
### 업체
스윗트래커
### 사용기술
JAVA, Objective C, PHP, Java Script, Scala
### 역할
설계 및 개발, 프로파일링을 통한 퍼포먼스 및 안정성 개선
### 성과
누적 다운로드수 580만, 실제 사용자 300만명이 사용하는 어플리케이션으로 성장하였으며 광고 및 빅데이터 수집으로 한달 약 1억원의 수익 창출
### 기술설명
#### 배송페이지
![메인 리스트](https://lh3.googleusercontent.com/oy41zNYELsw_Sj0G2Waa6QM_GhZLOjNtcyUBSdy_CWjynF5XNIPKRemPc-sfLBPjALV4KfrRQpYd)
![배송조회 페이지](https://lh3.googleusercontent.com/Xu54tI5qFN0-G02K-vOsVdFIb9lkYMs1ALHZ4tWJuQZyizNGTI-Gp7mun3aW6nQtBO_GbOwxb3PE)

스마트택배 메인은 RecyclerView 를 사용하여 UI를 구성하였다. 
사용자가 아이템을 클릭하게 되면 송장번호를 서버로 전송하게 되고 해당 운송장번호의 정보를 response로 받아서 UI로 표시한다.
배송완료가 안된 아이템들은 10분 주기로 알람을 실행하여 서버를 호출하며, 상품이 바뀌면 노티피케이션을 통해 사용자에게 배송상태가 바뀜을 알려준다.
#### 백업/복원
![백업 복원](https://lh3.googleusercontent.com/BXUziZ84sHPgt4by1g2K8308GeiXelzSZBTJe3o5uKFLy1gIMYctnm7AeZr0_WC52tl_p2hBv-Z4)

백업,복원의 경우에는 기기 변경같은 경우에 본인의 데이터를 미리 백업 후 복원 할 수 있는 기능으로, 배송내역과 쇼핑몰 불러오기 계정까지도 백업 복원할 수 있는 기능이다.

#### 쇼핑몰 불러오기
![enter image description here](https://lh3.googleusercontent.com/_lUI-66ThCVOkx-wzhGao-UUHWH8x6mdej2lCyJVxzN3kXDkCjkMxKmICKFVOE8yGWS13eTqJRPd)
![enter image description here](https://lh3.googleusercontent.com/WjefwuA5xa_TR98_hRW-L90YyBzuRxyu_4d0DLsH5q6CJxgbsraPnK7SjynpgJM_RK_MoTanIm4c)
![enter image description here](https://lh3.googleusercontent.com/KArbHE5EOw6SQPMhsXg5JRcWhxKx_jofz3878TPDOjBERtX9aBTUFfzTjXZ3hY5Axa7PC2rRdXPy)

쇼핑몰 불러오기의 경우, WebView를 이용하여 로그인을 시도 후 Cookie를 획득한다. 그 후 URLConnection Header에 해당 Cookie를 넣어 페이지를 크롤링하여 XML 규격으로 만들고 이걸 서버로 전달한다.
서버상에서는 해당 XML을 미리 만들어놓은 정규식을 이용하여 문자열 파싱을 하고, 이것을 JSON으로 가공하여 앱으로 내려준다.
앱에서는 해당 JSON을 GSON을 사용하여 인스턴스화 후 데이터베이스 저장 및 노티피케이션을 통해 사용자에게 안내해준다. 
해당 기능에 대해서는 iOS도 Objective C로 개발하여 현재 서비스 중에 있음.

#### SMS, 노티피케이션 송장번호 파싱
문자 혹은 노티피케이션 리스너가 호출이 되면 앱에서는 문자열에서 특수 문자를 제거하고 정규식을 이용하여 숫자 및 특정문구를 추출하여 사용자에게 노티피케이션을 통해 배송상태를 알려준다.
