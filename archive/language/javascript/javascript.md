# 33 JavaScript Concepts

> [33 Concepts Every JavaScript Developer Should Know](https://github.com/leonardomso/33-js-concepts)의 키워드를 바탕으로 자바스크립트에 대한 개념을 정리한다.

> (모든 내용이 포함되어 있지는 않지만) 아래 정리한 내용은 주로 2019~2020년쯤 정리한 것으로서, 많이 미흡한 부분들이 있다. 그래서 2022년에 예전보다는 성장한(?) 나의 개념을 바탕으로 새롭게 gitbook을 이용해서 정리하여 웹상에서 출판까지 해볼 생각이다.

<hr />

## 자바스크립트는 어떻게 작동할까?

- [Call Stack(호출스택)](./33concepts/callstack.md)

- [Execution Context(실행컨텍스트)](./33concepts/execution-context.md)

## 타입과 연산자

- [Expression vs Statement(표현식과 문장)](./33concepts/expression&statement.md)

- [Primitive Type](./33concepts/primitivetype.md)

- [Value Types and Reference Types](./33concepts/valueType-vs-referenceType.md)

- Implicit, Explicit, Nominal, Structuring and Duck Typing

  - [Type Coercion(형변환)](./33concepts/coercion.md)

- [Dynamic Type](./33concepts/dynamicType.md)

- [논리연산자( && 와 || )의 이해](./33concepts/logical_operator.md)

## 함수와 스코프

- 함수 범위, 블록 범위, 렉시컬(lexical) 범위

  - [Function Basic](./33concepts/function_basic.md)

  - [What is Scope](./33concepts/scope.md)

  - [Variables & Scope](./33concepts/variables_scope_hoisting.md)

  - [Arrow Function](./33concepts/arrowfunction.md)

- IIFE, Modules, Namespaces

- [Closures](./33concepts/closure.md)

- [High Order Functions](./33concepts/highOrderFunctions.md)

<br />

## 자바스크립트의 OOP

- this, call, apply, bind

  - [this for beginner](./33concepts/this.md)

  - [call() vs apply() vs bind()](./33concepts/call_apply_bind.md)

- new, 생성자, instanceof, 인스턴스

  - [new operator & constructor](./33concepts/constructor.md)

  - [instanceof](./33concepts/instanceof.md)

- 프로토타입의 상속과 체인

  - [Prototype Inheritance and Prototype Chain(프로토타입의 상속과 체인)](./33concepts/prototype.md)

- Object.create와 Object.assign

- 상속, 다형성, 코드의 재사용성

<br />

## 자바스크립트의 비동기

- [Promises](./33concepts/promises.md)

- async/await

<br />

## 함수형 프로그래밍

- map, reduce, filter

- 순수함수, 부수효과, 상태변이

- 부분 어플리케이션, 커링(Currying), Compose, Pipe

<br />

## 자바스크립트의 자료구조와 알고리즘

- 자료 구조

- 컬렉션과 생성기

- [Recursion](./33concepts/recursion.md)

- 함수 성능과 빅 오(Big-O) 표기법

- 알고리즘

<br />

## 자바스크립트 디자인 패턴

- 설계 패턴

- 클린 코드

<br />

## 기타

- 비트 연산자, 형식화 배열, 버퍼(배열)

- [DOM and Layout Trees](./33concepts/dom.md)
