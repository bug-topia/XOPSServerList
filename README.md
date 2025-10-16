# X Operation Server List implemented in a Node.js

도메인 종료로 인해 서버 리스트의 기능을 할 수 없게된 게임을 위해 만든 Node.js 기반 서버 리스트 서비스입니다.

본 프로젝트는 X Operations 게임의 서버 리스트 기능을 Node.js 기반으로 재구현한 서비스입니다. 기존 [http://cgil.plala.or.jp/](http://cgil.plala.or.jp/) 도메인이 종료됨에 따라 게임 내 서버 리스트 기능이 더 이상 작동하지 않게 되어, 이를 대체하기 위해 개발되었습니다.

기존 PHP 기반의 구현은 웹 서버 환경(Apache 등)에 의존하고 있었고, 유지 보수나 배포에 제약이 많았습니다. 반면 본 프로젝트는 Node.js의 특성을 활용하여 웹 서버 없이도 자체적으로 HTTP 요청을 처리하며, 경량이고 유연한 구조로 구현되었습니다.

## 서버-클라이언트 간 흐름 및 처리 방식
### 1. 클라이언트
클라이언트는 서버에 `HTTP GET` 요청을 보냅니다. 요청 URL과 쿼리 스트링에 따라 서버의 처리가 달라집니다.

#### 서버 리스트 조회
```swift
GET /~ninetwo/xopsolt/slsv.cgi HTTP/1.0
Host: 127.0.0.1
```

#### 서버 등록
```swift
GET /~ninetwo/xopsolt/slsv.cgi?MyServer&1234 HTTP/1.0
Host: 127.0.0.1
```

#### 서버 삭제
```swift
GET /~ninetwo/xopsolt/slsv.cgi?del HTTP/1.0
Host: 127.0.0.1
```

### 2. 서버
서버는 반드시 `HTTP GET` 요청을 받으며, 요청을 보낸 클라이언트의 IP 주소를 기록합니다.

#### 서버 리스트 조회
```text
로비메시지의 내용
5
192.168.0.1&1234&My Server 1
127.0.0.2&5678&Server
...
```
클라이언트로 부터 서버 리스트 조회 요청 수신 시 위 형식에 맞추어 값을 반환합니다.

## 목표
- [ ] 만료 시간 설정
- [ ] 국가 구분
- [ ] 초당 요청 횟수 제한 (과부하 방지)

## Reference
- [XOPS用サーバーリスト配信プログラム](https://gist.github.com/salty-godzilla/da8cc0efbe3eb0592522d3cec0c8bd15 "XOPS用サーバーリスト配信プログラム")
