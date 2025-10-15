# X Operation Server List implemented in a C# Console App

[http://cgil.plala.or.jp/](http://cgil.plala.or.jp/) 도메인 종료로 인해 서버 리스트의 기능을 할 수 없게된 게임을 위해 만든 C# 콘솔 앱 기반 서버 리스트 서비스입니다.

Reference의 링크 속 코드는 PHP로 작성되었으며, 웹 서버 환경에 크게 의존하는 구조입니다. 반면, 본 프로젝트는 별도의 웹 서버 없이 직접 HTTP 요청을 처리하여 보다 안정적이고 효율적인 서버 리스트 서비스를 제공합니다.

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

## Reference
- [XOPS用サーバーリスト配信プログラム](https://gist.github.com/salty-godzilla/da8cc0efbe3eb0592522d3cec0c8bd15 "XOPS用サーバーリスト配信プログラム")
