[< 뒤로가기](./README.md)

## [Cannot read properties of undefined (reading 'release')](https://github.com/Broccoli-Velog/Broccoli-Backend/issues/4)

- 작성일자 : `2022-08-xx`
- 작성자 : @unchaptered

<hr>

### 🔧 문제 발생 지점

프로젝트 초기에 `mysql` 을 설치하고 기본 코드를 작성하였습니다.

하지만, 해당 모듈이 비동기 코드가 지원되지 않는 부분이 있어서 `mysql2` 를 설치하고 마이그레이션 하였습니다.

그때부터 `Cannot read properties of undefined (reading 'release')` 에러가 시작되었습니다.

<hr>

### 🔧 예상 지점 1

초기에는 `mysql` 파일과 `mysql2` 호출 파일이 동시에 존재해서 에러가 뜨는 줄 알았습니다.

해당 `mysql` 파일에 `@deprecated` 처리를 하고 이후에 삭제하였습니다.

하지만, 이를 삭제했음에도 에러가 사라지지 않았습니다.

<hr>

### 🔧 에상 지점 2

기존의 코드에서는 파일 최상단에서 직접 호출 되는 방식이었습니다.

또 서버 실행 시점의 코드 전개가 불안정하다고 느꼈습니다.

```javascript
import mysql from "mysql2/promise";
const pool = mysql.createPool({
});

const connection = await pool.getConnect(0);
connection.release();
```

<hr>

### ⭕ 해결 방법

최상단 영역에서 사용되던 호출 함수들을 전부 클래스 안에 넣었습니다.

또한 `static` 타입의 pool 을 통해서 하나의 풀만 만들어지는 구조로 만들었습니다.

1. [Database Provider](https://github.com/Broccoli-Velog/Broccoli-Backend/blob/main/src/modules/providers/database.provider.js)
2. [Env Provider](https://github.com/Broccoli-Velog/Broccoli-Backend/blob/main/src/modules/providers/env.provider.js)