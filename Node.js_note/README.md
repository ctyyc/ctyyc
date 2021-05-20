## Node.js ?
    - Node.js 는 서버사이드 자바스크립트이며 구글의 자바스크립트 엔진인 V8을 기반으로 구성된 일종의 소프트웨어 시스템입니다.
    - 특징 : 싱글 스레드에 비동기 방식, 이벤트 기반의 Non-Blocking I/O
    - I/O 부하가 심한 대규모 서비스를 개발하기 적합
    - 기존에는 각 연결에 대해 새로운 쓰레드를 생성하고 그에 따라 메모리를 할당하여 사용자 요청을 처리했다면, 노드에서는 각 연결이 하나의 이벤트로서 노드 엔진에서 처리

###  Blocking I/O
    - 하나의 프로세스가 어떤 자원을 사용하고자 할 때 그 자원을 다른 프로세스가 점유하고 있다면, 그 프로세스가 그 자원의 사용을 끝마칠 때까지 기다려야 한다는 것
    - 멀티 쓰레드를 사용 시, 스케줄링을 위한 처리 시간과 Context seitch 비용이 발생하는 문제점이 있다.

    - 싱글 쓰레드를 가진 노드는 I/O 작업이 시작되면 I/O 작업 처리에 대한 응답을 기다리지 않고, 바로 다음 작업을 실행해버립니다. 대신 I/O 작업이 종료되면 이벤트를 발생시키고, 이 이벤트는 해당 프로세스의 이벤트 큐에 등록되게 됩니다. 노드로 개발된 프로세스는 이 이벤트 큐에 등록된 새로운 이벤트를 감지하여, 해당 이벤트 시 수행하여야 할 작업을 실행하게 됩니다. 

### 이벤트 루프(Event Loop)
    작업을 요청하면서 그 작업이 완료되었을 때 어떤 작업을 진행할지에 대한 콜백 함수를 지정하여 동작이 완료되었을 때 해당 콜백 함수를 실행되는 방식의 동작 방식 (어떤 요청이 발생하면 그 작업에 대해 쓰레드 실행만을 일으킨다.)

### 모듈
    - 애플리케이션을 이루는 기본 조각
    - require() 메소드를 통해 가져오며, module.exports로 외부에서 사용할 수 있도록 허용

### Node.js 상속
    util 모듈을 사용하여 상속
```
util.inherits(B, A); // B가 A를 상속받음
```

#### 관련 명령어
```
$ npm list -g                   // 글로벌로 설치된 모듈 확인
$ npm update [modules name] -g  // 글로벌로 설치된 모듈 업데이트 
$ npm uninstall [modules name]  // 삭제
```

### package.json
    배포한 모듈의 정보를 담는 json 파일, 프로젝트에서는 확장 모듈에 대한 의존성 관리가 가능하다.

### express-generator
```
express --view=pug myapp
```

### 라우터
    express에서 '라우팅'이라는 개념은 클라이언트로부터 요청받은 URL과 뷰를 매칭시키는 것

### 미들웨어
    - 자기가 수행 할 부분을 수행하고 다음 과정으로 진행을 넘기는 것을 의미합니다.
    - 미들웨어를 사용하는 이유는 어떤 미들웨어에서 req, res 객체에 속성 또는 메서드를 추가했을 때, 다른 미들웨어서도 이전 미들웨어에서 추가한 req, res 객체의 속성 또는 메서드를 사용할 수 있기 때문입니다.

### 클라이언트/서버 통신 방식
    - Polling 방식 : 클라이언트가 서버에 주기적으로 요청 후 응답을 받는 방식
    - Long Polling 방식 : Client가 서버에 대한 요청을 유지하여 반복적인 요청을 없애고 유효한 이벤트가 발생하면 응답을 해주는 방식
    - WebSocket 방식 : 클라이언트와 서버의 양방향 연결 채널 구성 (Socket.io를 이용하여 구 버전도 사용 가능)

### ORM(Object Relational Mappings)
    - 프로그램 상의 객체(Object)와 DB의 테이블(Relation)이 일대일 대응하는 관계를 맺는 것(Mapping)을 의미합니다.
    -bORM을 이용하면 query가 아닌 메서드로서 데이터를 조작할 수 있다는 것이 큰 장점입니다.
    -bORM의 특징은 특정 DB에 종속되지 않는다는 것입니다.

### Sequelize
    Node.js기반의 ORM으로 Promise 문법을 사용합니다.
```
npm install sequelize mysql2
npm install -g sequelize-cli
sequelize init
```

#### cli로 model 생성
```
sequelize model:create --name TABLE_NAME --attributes "COLUMN1:type, COLUMN2:type, COLUMN3:type"
```

### Migration
- "up"기능과 "down"기능을 가진 일련의 데이터베이스 작업입니다.(up은 변경, down은 복원)

#### 컬럼 수정 후
```
sequelize db:migrate 
```

#### 마이그레이션 이후 모델을 수정한 경우,
```
sequelize db:migrate:undo // 이후 마이그레이션 파일 변경
```

### method-override
    method-override 모듈은 put, delete 방식을 지원한다.

### 클라이언트에서 넘어온 매개변수 받는 방법

#### URL 파라미터
    - req.params.변수명
    - 이 방식은 게시글 수정과 삭제 할 때 사용했던 방법인데, URL에 동적인 데이터를 추가하는 방식입니다.
    ex) 라우터를 등록할 때 app.get( /post/:postid ) 으로 경로를 설정했다면, 클라이언트에서 "/post/3"으로 요청 시, req.params.postid == 3 입니다.

#### query 파라미터
	- req.query.키
	- URL 파라미터 방식과 같이 URL을 통해서 데이터를 얻을 수 있지만, query string의 key 값을 받아올 수 있습니다.
	ex) 클라이언트에서 "/post?postid=3"으로 요청 시, req.query.postid == 3 입니다.

#### form 파라미터
	- req.body.name이름
	- HTML form 태그를 통해 넘어온 데이터를 받는 방법입니다.
	ex) 클라이언트에서 input 태그의 name="title" 일 때, "victolee"를 입력하고 전송 버튼을 누르면 req.body.title == vcitolee 입니다.


<br/>
<br/>
이 글은 '한 눈에 끝내는 Node.js'와 'victolee'님의 블로그를 참고하였습니다.