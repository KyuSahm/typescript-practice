## Typescript
- 브라우저는 typescript를 인식 못함
  - typescript로 짠 코드를 javascript로 변환해야 함
- [TypeScript Playground](https://www.typescriptlang.org/play)
  - TypeScript를 코딩한 후, 변경된 Javascript를 바로 확인 가능
- ``node.js``를 이용하는 방법
  - typescript 패키지를 설치
  - tsc를 이용하여 typescript를 javascript로 변환
  - javascript 실행
```bash
$npm install -g typescript
$tsc index.ts
gusam@DESKTOP-RF6D56E MINGW64 /d/Workspace/typescript-practice (main)
$node index.js
[ 'z', 1, 2 ]
```

### Typescript를 사용하는 이유
- 아래와 같이, javascript에서는 인자를 전달하지 않아도 에러가 발생하지 않음
  - ``NaN = undefined + undefined``
  - ``NaN = number + undefined``
```javascript
function add(num1, num2) {
    console.log(num1 + num2);
}

add();
add(1);
add(1, 2);
add(3, 4, 5);
add('hello', ' world');
```
```bash
$node index.js 
NaN
NaN
3
7
hello world
```
- Javascript는 동적언어
  - 런타임에 타입 결정 및 오류 발견 가능
```javascript
function showItems(arr) {
    arr.forEach(item => {
        console.log(item);
    });
}

showItems([1, 2, 3]);
showItems(1, 2, 3);
```
```bash
$node index.js 
1
2
3
D:\Workspace\typescript-practice\index.js:2
    arr.forEach(item => {
        ^

TypeError: arr.forEach is not a function
    at showItems (D:\Workspace\typescript-practice\index.js:2:9)
    at Object.<anonymous> (D:\Workspace\typescript-practice\index.js:8:1)
    at Module._compile (node:internal/modules/cjs/loader:1101:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1153:10)
    at Module.load (node:internal/modules/cjs/loader:981:32)
    at Function.Module._load (node:internal/modules/cjs/loader:822:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:81:12)
    at node:internal/main/run_main_module:17:47
```
- Java, TypeScript는 정적 언어
  - 컴파일 타임에 타입 결정 및 오류 발견     
- TypeScript에서 Javascript 예제를 적용하면, 아래 이미지처럼 타입을 체크해 줌

![typescript_1.png](./images/typescript_1.png)
- Typescript를 적용하면, 아래와 같이 수정해야 함
```javascript
function add(num1:number, num2:number) {
    console.log(num1 + num2);
}

//add();
//add(1);
add(1, 2);
//add(3, 4, 5);
//add(1, ' world');
```
```javascript
function showItems(arr:number[]) {
    arr.forEach(item => {
        console.log(item);
    });
}

showItems([1, 2, 3]);
//showItems(1, 2, 3);
```
### Typescript의 기본 타입
#### 기본 타입과 배열 그리고, Tuple
```javascript
// Basic types: string, number, boolean
let car:string = 'bmw';
let age:number = 30;
let isAdult:boolean = true;

// Array
let a1:number[] = [1, 2, 3];
let a2:Array<number> = [1, 2, 3];
let week1:string[] = ['mon', 'tue', 'wed'];
let week2:Array<string> = ['mon', 'tue', 'wed'];

// Tuple
let b:[string, number, number];
b = ['z', 1, 2];
b[0].toLowerCase();
//b[1].toLowerCase();
console.log(b);
```
#### 함수의 반환 타입
- 반환하지 않는 경우
```javascript
function sayHello():void {
    console.log('hello');
}

sayHello();
//let a:string = sayHello();
```
- 에러를 Throw하거나, 무한 루프인 경우
```javascript
function showError():never {
    throw new Error();
}

function infLoop():never {
    while (true) {
        // do something...
    }
}
```
#### enum type
##### 숫자를 사용한 enum type
- ``index.ts``
```javascript
enum Os {
    Windows,
    Ios = 4,
    Android
}

let myOs:Os = Os.Windows;

console.log(Os[4]);
console.log(Os["Ios"]);
```
- ``index.ts``를 tsc로 수행한 결과
```javascript
"use strict";
var Os;
(function (Os) {
    Os[Os["Windows"] = 0] = "Windows";
    Os[Os["Ios"] = 4] = "Ios";
    Os[Os["Android"] = 5] = "Android";
})(Os || (Os = {}));
let myOs = Os.Windows;
console.log(Os[4]);
console.log(Os["Ios"]);
```
- 수행 결과
```bash
$tsc index.ts
$node index.js
Ios
4
```
##### 문자열을 사용한 enum type
- ``index.ts``
```javascript
enum Os {
    Windows = 'win',
    Ios = 'ios',
    Android = 'and'
}

let myOs:Os = Os.Windows;
console.log(myOs);
```
- ``index.ts``를 tsc로 수행한 결과
```javascript
var Os;
(function (Os) {
    Os["Windows"] = "win";
    Os["Ios"] = "ios";
    Os["Android"] = "and";
})(Os || (Os = {}));
var myOs = Os.Windows;
console.log(myOs);
```
- 수행 결과
```bash
$tsc index.ts
$node index.js
win
```
##### null, undefined type
- ``index.ts``
```javascript
let a:null = null;
let b:undefined = undefined;
```
- ``index.ts``를 tsc로 수행한 결과
```javascript
var a = null;
var b = undefined;
```



