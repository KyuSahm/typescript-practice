## Typescript
- 브라우저는 typescript를 인식 못함
  - typescript로 짠 코드를 javascript로 변환해야 함
- [TypeScript Playground](https://www.typescriptlang.org/play)
  - TypeScript를 코딩한 후, 변경된 Javascript를 바로 확인 가능

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