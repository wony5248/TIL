# typeScript npm 패키지 만들기
#### 프로젝트 생성 및 세팅
* npm 사이트에 접속하여, 중복되지 않는 라이브러리 이름을 정한다.
* 해당 라이브러리 이름으로 directory를 생성한다.
* 해당 dir로 이동하여 npm init 명령어를 통해 npm 관련 설정을 해준다.
* package.json에 아래의 설정을 추가한다.
```
{
  ...,
  "type": "module",
}
```
* typeScript를 설치한다. (npm i typescript)

#### ts 모듈 개발
* src 폴더를 만들고 그 안에 index.ts 모듈을 작성한다.

#### ts 모듈 컴파일
* ts 파일을 컴파일 하여 dist dir에 저장되도록 한다.
* commonJS 형식으로 한번, ESModule 형식으로 한번 컴파일 해주기 위해 루트 디렉토리에 3개의 tsconfig 파일을 만들어 준다.
```
├── tsconfig-base.json
├── tsconfig-cjs.json
└── tsconfig.json
```
* tsconfig-base.json
```
{
  "compilerOptions": {
    "target": "ES5",
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "baseUrl": "src",
    "declaration": true,
    "esModuleInterop": true,
    "inlineSourceMap": false,
    "listEmittedFiles": false,
    "listFiles": false,
    "moduleResolution": "node",
    "noFallthroughCasesInSwitch": true,
    "pretty": true,
    "resolveJsonModule": true,
    "rootDir": "src",
    "skipLibCheck": true,
    "strict": true,
    "traceResolution": false
  },
  "compileOnSave": false,
  "exclude": ["node_modules", "dist"],
  "include": ["src"]
}
```
* tsconfig-cjs.json
```
{
  "extends": "./tsconfig-base.json",
  "compilerOptions": {
    "module": "commonjs",
    "outDir": "dist/cjs",
    "target": "es2015"
  }
}
```
* tsconfig.json
```
{
  "extends": "./tsconfig-base.json",
  "compilerOptions": {
    "module": "esnext",
    "outDir": "dist/mjs",
    "target": "esnext"
  }
}
```
* 해당 config 파일들 작성 이후 fixup.sh라는 스크립트 파일을 만든다.
* fixup.sh
```
cp dist/mjs/index.d.ts dist 

rm -rf dist/*/index.d.ts 

cat >dist/cjs/package.json <<!EOF
{
    "type": "commonjs"
}
!EOF

cat >dist/mjs/package.json <<!EOF
{
    "type": "module"
}
!EOF
```
#### package.json 수정
* script 실행 명령어 set
```
{
  "scripts": {
    "build": "rm -fr dist/* && tsc -p tsconfig.json && tsc -p tsconfig-cjs.json && ./fixup.sh"
  },
}
```
* export 관련 설정
```
{
  ...,
  "main": "dist/cjs/index.js",
  "module": "dist/mjs/index.js",
  "types": "dist/index.d.ts",
  "exports": {
    ".": {
      "import": "./dist/mjs/index.js",
      "require": "./dist/cjs/index.js"
    }
  },
}
```
#### .npm 에 배포
* npm run build를 통해 해당 ts 파일을 build 해준다.
* npm publish를 통해 해당 패키지를 npm에 배포한다.
* 새로 배포할 경우 package.json의 버전을 변경한뒤 npm publish를 해준다.
