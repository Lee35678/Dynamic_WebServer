# Dynamic_WebServer

Python 표준 라이브러리 `http.server`로 만든 간단한 HTTP 서버. GET 요청에는 요청 경로를 담은 HTML을, POST 요청에는 본문을 파일로 저장하고 JSON 상태를 돌려준다.

## 개요

`myWeb.py` 한 파일로 된 실습용 웹 서버다. `BaseHTTPRequestHandler`를 상속한 `MyServer` 클래스가 GET과 POST를 처리하며, 요청 경로에 따라 응답이 달라지는 동적 응답 구조를 익히는 것이 목적이다.

## 동작 방식

- 바인딩: `hostName`(`localhost`), `serverPort`(8000)
- 시작 시 `Server started http://localhost:8000` 출력, `Ctrl+C`로 종료하면 `Server stopped.` 출력

| 메서드 | 경로 | 동작 |
|--------|------|------|
| GET | 모든 경로 | 200 응답. `Request: <요청 경로>`와 `This is an example web server.`를 담은 HTML |
| POST | `/` | 200 응답, 본문 `{"status":"ng"}` |
| POST | 그 외 경로 (예: `/data.txt`) | 요청 본문을 콘솔에 출력하고 `{"status":"ok"}` 응답, 본문을 현재 폴더의 같은 이름 파일(`.` + 경로)에 저장 |

- POST 처리 중 예외(예: `Content-Length` 헤더 없음)는 무시된다

## 개발 환경

- Python 3
- 표준 라이브러리만 사용: `http.server` (`BaseHTTPRequestHandler`, `HTTPServer`), `time`

## 설정

`myWeb.py` 상단의 변수로 바인딩 주소와 포트를 바꾼다.

- `hostName` : 기본값 `localhost`라서 같은 PC에서만 접속된다. 다른 기기(예: ESP32)에서 접속하려면 바꿔야 한다
- `serverPort` : 기본값 8000

## 빌드 및 실행

```bash
python myWeb.py
```

동작 확인 예시:

```bash
curl http://localhost:8000/hello
curl -X POST --data "hello" http://localhost:8000/test.txt
```

두 번째 명령을 실행하면 서버를 실행한 폴더에 `test.txt`가 만들어진다.

## 폴더 구조

```
Dynamic_WebServer/
└── myWeb.py   # GET/POST 처리 HTTP 서버
```
