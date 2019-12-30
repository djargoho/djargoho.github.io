---
title: "React Native App을 위한 local Database 선택"
subtitle: "Local Database 무엇을 골라야 할까?"
layout: post
author: "DJArgoho"
date: 2019-12-31 02:00:00
# header-style: text
tags:
  - ReactNative
  - LocalDatabase
  - Database
  - Realm
  - Firebase
  - SQLite
  - PouchDB
---

## 로컬 데이터 베이스 무엇을 골라야 할까

> &nbsp;
> 공부를 하며 정리한 글입니다.  
> 부족한 글 혹은 잘못된 내용이 있을 수도 있으니 다른 블로그 글들을 보시거나 참고만 해주세요.
> &nbsp;

모바일 앱을 개발하고, 서버(Server)의 부담을 줄이기 위해서는 로컬 데이터베이스는 필수 불가결이라고 볼수 있다.  
그 중 React Native에서 많이 사용하는 Local Database를 볼 3가지를 정리해 봤다.  
하지만 그 전에 Local Database로써 무엇이 필요한 지 살펴보자.  

## App을 위해 따져야할 Local Database 선택 요소

**1. 오프라인 동기화를 지원**
**2. 데이터베이스의 보안수준**
**3. 읽기/쓰기 속도**
**4. 지원하는 데이터 타입**
**5. 가격**
**6. 실시간 동기화 지원**

## Local DataBase

### 1. Realm

![Realm logo](../../img/reactNative/realm_logo.jpg  =250x)

Realm은 SQLite에 대한 모바일 데이터베이스 대체제라 볼 수 있다.  
그리고 자체 엔진을 쓰면서 Native NoSQL Database이기 때문에 SQLite보다 빠른 속도를 가진다.
( SQLite는 ORM형 database, Realm은 기존의 mobile database형태가 다르다는 걸 알 수 있다. )  

자체 C++ Core를 가지고 있으며,
Realm의 목적은 SQLite의 모바일 데이터 베이스의 대체제를 제공하는 걸 목적으로 하고 있다.  

Benchmark에 따르면 SQLite database(SQLite 튜닝 안했을 시)보다 기본적인 호출을 했을 때,  
약 10배의 빠른 속도를 보여준다고 한다.  

문서형으로 되어있다보니, ORM인 SQLite보다 즉각적인 데이터의 저장 및 생성이 편리하다.  
또한 JSON, 다양한 API, Data 변경 Noti, 암호화 등 최신 db의 특성을 다 가지고 있다.  

#### 참고

> 현재 Realm과 mongo DB와 같이 MongoDB Realm이라는 solution을 만드는 중이라고 한다.  
> Realm의 database 기술과 MongDB stitch라는 serverless platform에 합쳐진 솔루션.
> 2020년에 배포 예정이라고 한다. 아래는 해당 링크이다.  
> &nbsp;
> 참고 링크 : <https://www.mongodb.com/realm#roadmap>  

### 2. Firebase

![Firebase logo](../../img/reactNative/firebase_logo.png)

NoSQL cloud database에 데이터를 동기화하고 저장한다.  
데이터는 모든 클라이언트에 실시간으로 동기화되고 오프라인일 때도 해당 앱에 데이터가 남아있다.  

Firebase는 클라우드에 호스팅된 실시간 데이터베이스이며,  
해당 데이터는 JSON 형태로 저장 및 연결된 모든 클라이언트에 실시간으로 동기화 된다.  
iOS, Android, javascript SDK 등 크로스 플랫폼을 구상중이면,
해당 모든 환경에 방해받지 않고 Client들은 하나의 실시간 Database 인스턴스를 공유할 수 있다.  
그리고 자동으로 최신 데이터로 업데이트 된다.  

하지만 데이터 타입이 제약적이거나, 트래픽이 올라가면 가격이 비싸진다는 문제가 있다.  

### 3. SQLite

![SQLite logo](../../img/reactNative/SQLite_logo.png)

SQLite는 디바이스에 데이타를 텍스트 파일로 저장하는 오픈소스 SQL Database이다.
모든 관계형 데이터베이스의 특성들을 지원하고 있고,  
해당 database에 접근하기 위해서 JDBC, ODBC같은 connection lib를 필요로 하지 않는다.  
단, Database를 만들거나 업데이트하기 위해서 해당 statement를 작성해야한다.  

NoSQL database보다는 느리기 때문에, 비동기 환경에서 해당 database를 구동되는 게 추천 된다.  

### 결론

선택시 고려할 것.

#### Firebase

- 데이터 타입이 단순,명료.
- 소규모 앱
- 온라인 동기화까지 고려
- 트래픽이 적다.
- 배우기 쉬움
- NoSQL

#### Realm

- Local DB 목적으로는 최적. (Cloud platform은 무조건 돈 받는다.)
- 빠른 속도
- 배우기 쉬움
- NoSQL

#### SQLite

- 관계형 DB
- 완전 무료, 오픈 소스
- ORM DB에 익숙한 사람 (SQL문)
