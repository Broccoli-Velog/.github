[< 뒤로가기](./README.md)

## [Doen't work 'npm run dev' on terminal](https://github.com/Broccoli-Velog/Broccoli-Backend/issues/5)

- 작성일자 : `2022-08-06`
- 작성자 : @codeing999

# NPM RUN DEV 명령어 에러 이슈

## 문제

```
//package.json
  "scripts": {
    "start": "NODE_ENV=prod node ./src/index.js",
    "dev": "NODE_ENV=dev nodemon ./src/index.js"
  },
````
package.json 파일에 이와 같이 작성하였었는데
프로젝트 같이하는 다른 분들은 잘 작동하는데 나만 안되었다.


## 해결
```
//package.json
  "scripts": {
    "start": "set NODE_ENV=prod&& node ./src/index.js",
    "dev": "set NODE_ENV=dev&& nodemon ./src/index.js"
  },
````
슬렉에 질문을 올려서 해결되었다. 
먼저 windows 사용 중이냐고 물어보신걸 보니 windows와 관련된거같은데
windows에서 환경변수 설정할 때 set을 쓰는 것과 관련된 것 같다.
그러나 다른 분들도 다 windows 쓰는데 왜 나만 안됐던건지는 모르겠다.
