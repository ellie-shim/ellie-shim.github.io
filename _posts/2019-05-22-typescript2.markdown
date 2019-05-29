---
layout: post
title: "TypeScript - 2. 타입스크립트 개발환경 구축"
subtitle: "타입스크립트 개발환경 구축"
categories: dev
tags: TypeScript
comments: true
---

TypeScript 파일(.ts)은 브라우저에서 동작하지 않으므로 TypeScript 컴파일러를 이용하여 자바스크립트 파일로 변환해야 합니다. 이 작업을 컴파일 또는 트랜스파일링이라고 합니다.

## 1. Node.js

[Node.js의 웹사이트에서 설치할 수 있습니다.](http://nodejs.org)

## 2. TypeScript 컴파일러 설치 및 사용법

### 2.1 TypeScript 컴파일러 설치

npm을 사용하여 TypeScript를 전역에 설치해줍니다.

```bash
$ npm install -g typescript
```

> 권한 오류시 sudo를 이용할 수 있습니다. sudo npm install -g typescript

TypeScript의 버전을 확인해 볼 수 있습니다

```bash
$ tsc -v
Version 3.4.5
```

TypeScript 컴파일러(tsc)는 TypeScript 파일(.ts)를 자바스크립트 파일(.js)로 트랜스파일링 합니다.

### 2.2 TypeScript 컴파일러 사용법

#### 기본 트랜스파일링

TypeScript 파일(.ts)을 만들어 코드를 작성하고 터미널에 아래의 명령어를 입력하면 트랜스파일링 됩니다. 이때 확장자 .ts는 생략할 수 있습니다.

`ellie.ts` 파일을 트랜스파일링 할 때

```bash
$ tsc ellie
```

트랜스파일링이 완료되면 같은 디렉토리에 자바스크립트 파일(ellie.js)가 생성됩니다.

#### 자바스크립트 버전 설정

기본적으로 ES3버전으로 컴파일링 되는데 `--target`이나 `-t`를 사용해서 자바스크립트 버전을 변경할 수 있습니다.

현재 tsc가 지원하는 자바스크립트 버전은 ES3, ES5, ES6(ES2015), ES2016, ES2017(ESNext)입니다.

```bash
$ tsc ellie -t es6
```

#### 여러개의 파일 트랜스파일링

파일명을 연달아 입력하거나 \*.ts를 이용하여 한꺼번에 트랜스파일링이 가능합니다.

`ellie.ts`, `siotz` 파일을 트랜스파일링 할 때

```bash
$ tsc ellie siotz
// 또는
$ tsc *.ts
```

[TypeScript Compiler Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html)에서 더 많은 옵션을 확인할 수 있습니다.

## 3. Visual Studio Code에서의 TypeScript

VSCode는 마이크로소프트가 제공하는 오픈소스 코드 에디터입니다. TypeScript도 마이크로소프트에서 개발했기 때문에 VSCode는 TypeScript를 잘 지원하고있습니다. IntelliSense, debugging, Git 등의 기능을 지원하며 다양한 Extension(확장 플러그인)을 제공하여 자신의 프로젝트에 맞는 개발 환경을 쉽게 구축할 수 있습니다.

### 3.1 tsconfig.json

트랜스파일링 할 때마다 `tsc ellie -t es6`와 같은 옵션을 입력해주는 것은 매우 번거로운 일이므로 `tsconfig.json`을 이용하여 트랜스파일링에 대한 기본 설정을 해주는 것이 좋습니다.

#### compilerOptions

해당 프로퍼티에는 트랜스파일링 옵션을 설정할 수 있습니다. 생략한 경우에는 기본 트랜스파일링 옵션이 사용됩니다.

```json
{
  "compilerOptions": {
    "target": "ES5",
    "module": "commonjs",
    "sourceMap": true
  }
}
```

#### files, include, exclude

컴파일 대상 파일을 지정하기 위해서 `files` 또는 `include` 프로퍼티를 사용합니다. 만약 `files` 프로퍼티를 정의하였다면 `include` 프로퍼티는 무시됩니다.

`files` 프로퍼티에는 컴파일 대상 파일의 상대 경로 또는 절대 경로를 명시적으로 설정합니다.

```json
{
  "files": ["src/ellie.ts", "src/siotz.ts"]
}
```

`include` 프로퍼티에는 컴파일 대상 파일 리스트를, `exclude` 프로퍼티에는 컴파일 대상에서 제외할 파일 리스트를 설정합니다.

```json
{
  "include": ["src/**/*"],
  "exclude": ["node_modules", "**/*.spec.ts"]
}
```

최종적으로 tsconfig.json 파일은 아래와 같습니다.

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES5",
    "module": "commonjs",
    "sourceMap": true
  },
  "include": ["ellie.ts", "siotz.ts"],
  "exclude": ["node_modules"]
}
```

### 3.2 Configure Task

외부에 존재하는 TypeScript 컴파일러와 VSCode의 연동이 필요하다

`command + shift + p`로 명령 팔레트를 선택하고 `tasks : configure task`를 입력 선택한다
![configure task](https://ellie-shim.github.io/assets/img/ts1.png)

`tsc`를 입력하여 `tsc : 빌드-tsconfig.json`을 선택한다.
![tsc:빌드](https://ellie-shim.github.io/assets/img/ts2.png)

.vscode라는 숨겨진 풀더에 `tasks.json` 파일이 생성된다.

`command + shift + B` 단축키로 `tsc : 감시`를 실행하게되면 컴파일이 진행된다.

## 참고

[Poiemaweb-Typescript 개발환경 구축](https://poiemaweb.com/typescript-introduction#3-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95)
[Poiemaweb-TypeScript Visual Studio Code Setup](https://poiemaweb.com/typescript-vscode)
