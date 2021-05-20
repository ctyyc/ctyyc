## Nest.js?
    Node.js의 프레임워크이다. (express와 fastify 프레임워크 기반으로 동작)

```
npm i -g @nestjs/cli
nest new project-name
```

### 데코레이터
    - 클래스에 함수 기능을 추가할 수 있음 (어노테이션과 비슷한 개념?)
    ex. @Get, @Post, @Delete, @Put(전체 업데이트), @Patch(부분 업데이트)

### 구조
    - 컨트롤러는 url을 가져오고 함수를 실행함(Node.js의 router와 같은 개념)
    - 서비스에서 비지니스 로직을 실행
```
nest g co		// 컨트롤러 생성
nest g s		// 서비스 생성
nest g mo       // 모듈 생성
```

### async/await
    async/await를 사용하려면 promise 객체를 반환해야 한다.

### dto를 사용하는 이유
    코드를 간결화하고, 유효성을 체크하기 위해

### 유효성 체크 관련 라이브러리
    - class-validator : 유효성 체크 라이브러리
    - class-transformer : 입력된 데이터 타입을 알맞는 데이터 타입으로 변환
```
npm install class-validator class-transformer
```

### mapped-types
타입을 자동으로 변환시켜 사용할 수 있게 도와주는 라이브러리 
```
npm install @nestjs/mapped-types
```

### DI
    Nest.js가 대신 import 해주는 것 ..?

## Test
    - Unit test와 e2e test가 있다.
    - Unit test는 하나의 모듈?함수? 단위로 테스트
    - e2e(end to end) test는 전체를 테스트

    - 기본적으로 .spec.ts 파일로 테스트
```
npm run test:watch
npm run test:cov
npm run test:e2e
```

### Test 코드 구조
    describe > it > request().get().expect()
    todo    // 구현해야할 코드



<br/>
<br/>
이 글은 '노마드 코더'님의 블로그를 참고하였습니다.