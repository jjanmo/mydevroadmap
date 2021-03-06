# Type Conversion(타입변환/형변환)

> 정리의 기본적인 순서는 [JavaScript type coercion explained](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/) 를 참고하여 작성하였습니다.

- 자바스크립트는 [동적타이핑](dynamicType.md) 언어 혹은 `느슨한타입(loosely typed)` 언어이다. 그렇기 때문에 변수의 타입을 미리 선언할 필요가 없다. 또한 변수에 여러 타입을 할당하는 것이 가능하다. 이러한 이유로 자바스크립트는 상황에 맞게 자동적으로 형변환을 하는 경우가 있다. 이러한 형변환을 `암묵적 타입 변환(Implicit coercion)`이라고 한다. 이와는 다르게 개발자가 의도적으로 형변환을 명시하는 경우가 있다. 이를 `명시적 타입변환(Explicit coerion)`이라고 한다.

- **암묵적 타입변환**은 어떠한 기준을 두고 그 기준에 맞게 형변환을 시킨다. 그 기준이라함은 바로 `문맥(context)`이다. 예를 들어 어떤 표현식(expression)에서는 숫자가 기대된다면 문자열을 숫자로 형변환하고, 다른 표현식에서 문자열이 기대된다면, 거기서는 숫자일지라도 문자열로 변환된다.

- 자바스크립트에서는 2가지 비교방법인 `==(형변환 비교)`와 `===(엄격한 비교)` 가 있다. `===`의 경우는 암묵적 타입 변환을 허용하지 않는다. 그렇기 때문에 피연산자의 자료형(타입)과 내용 모두 일치해야 참이 된다. 하지만 `==`의 경우는 비교 전에 필요하다면 같은 자료형(타입)으로 변환 후에 내용을 비교한다. (===와 ==대해선 다시 다룰 예정이다.)

- 암묵적 타입변환은 **양날의 검(double edge sword)** 라고 한다. 개발자의 의도와는 맞지않게 자동 형변환으로 인해 예측하지 못한 오류가 일어나기도 하지만, 자동 형변환으로 더 가독성 좋은 코드를 구현할 수 있다. 명시적 타입변환이든 암시적 타입변환이든 중요한 것은 내가 작성한 코드를 명확하게 이해할 수 있게 하는 것이다. 어떤 타입 변환이 더 가독성이 좋을지를 고민하는게 무엇을 선택하여 코딩할 것인가에 대한 기준이 될 것이라 생각한다.

## Preview

> 아래의 퀴즈에 대해서 다 대답할 수 있다면 당신은 타입 변환 마스터입니다 😎

```javascript
true + false
12 / "6"
"number" + 15 + 3
15 + 3 + "number"
[1] > null
"foo" + + "bar"
'true' == true
false == 'false'
null == ''
!!"false" == !!"true"
[‘x’] == ‘x’
[] + null + 1
[1,2,3] == [1,2,3]
{}+[]+{}+[1]
!+[]+[]+![]
new Date(0) - 0
new Date(0) + 0
```

> 정답은 맨 밑에 있습니다.

## 타입변환의 규칙

- 타입변환은 **3가지** 타입으로 일어난다. `to String, to Boolean, to Number`
- `원시자료형`과 `객체`는 타입변환이 일어나는 양상이 조금 `다르다`.

## 원시자료형

1. to String

- 명시적 타입변환 : `String()`를 사용

  > 모든 원시자료형은 String()을 사용하면 예상가능한 결과값(원시자료형 그대로의 값)을 얻을 수 있다.

  ```javasciprt
  String(123) //'123'
  String(null) //'null'
  String(undefined) // 'undefined'
  String(true) // 'true'
  ```

- 암묵적 타입변환 : `+` 연산자 사용

  > `+` 는 2가지 기능이 있다. 숫자만 있는 표현식에서는 일반적으로 알고 있는 `더하기 연산`을 한다. (문자열이 아닌 원시자료형의) 피연산자 연산은 자료형을 숫자로 변형해서 연산한다. 하지만 표현식 안에 문자열이 같이 있는 연산이라면 `+`는 더하기가 아니라 `결합`이라는 기능을 하게 된다. 즉 숫자를 자동으로 문자열로 바꿔서 문자열과 문자열이 결합한 결과를 나타낸다. 또한 하나의 표현식에 연산이 여러 개가 존재할 때, 어떤 연산에서 문자열로 결합이 일어나면 그 뒤로는 계속 결합이 일어난다.

  📌 `+` 연산자의 결합으로 사용될 때의 몇가지 규칙

  1. 피연산자 중 문자열이 1개라도 있다면 그 연산은 결합이 된다.
  2. 피연산자 중에 객체가 있다면 그 객체가 문자열로 바뀔수 있다면 다른쪽 피연산자도 문자열로 바꿔서 결합한다. 만약에 다른쪽 피연산자가 문자열로 형변환이 안된다면 모두 숫자로 형변환하여 연산한다.
     > 객체 형변환 내용은 객체부분에서 다시 정리됩니다.

  ```javascript
  //더하기
  1 + 2; // 3
  //결합
  1 + '2'; // '12'
  55 + 'javascript'; // '55javascript'
  1 + 3 + '3'; // '43'
  '1' + 3 + 3; // '133'
  1 + {}; //"1[object Object]"
  true + new Date(); // "trueThu May 21 2020 01:20:31 GMT+0900 (대한민국 표준시)"
  ```

1. to Boolean

   > 불리언값에는 `true`와 `false`가 있다. 그렇기 때문에 어느 값이 `true`로 혹은 `false`로 형변환이 가능한지를 아는 것이 중요하다. 자바스크립트에는 `falsy value`라는 것이 있다. `falsy value`는 자바스크립트 언어에서 `false와 동치인 값`을 말한다. 이 **falsy value를 제외한 모든 값**은 `true로 형변환이 가능`하다. 원시자료형이 아닌 객체들도 모두 `truthy value`로 true로 형변환이 가능하다. `빈객체({})`와 `빈배열([])` 역시 마찬가지이다.

   ```javascript
   //falsy value
   ''; //빈문자열
   0 - 0;
   NaN;
   null;
   undefined;
   false;
   ```

- 명시적 타입변환 : `Boolean()`을 사용

  ```javascript
  Boolean(1); //true
  Boolean(100); //true
  Boolean('string'); //true
  Boolean([]); //true
  Boolean({}); //true
  Boolean(''); //false
  Boolean(NaN); //false
  Boolean(undefined); //false
  Boolean(0); //false
  ```

- 암묵적 타입변환
  > 불리언타입이여야하는 문맥인지 아닌지에 따라서 타입변환이 일어난다. `if조건문, 논리연산자(&&, ||)`등이 있는 상황을 예로 들 수 있다. 이러한 상황에서 `falsy value`는 `false`로 `truthy value`는 `true`로 타입변환이 일어난다.

3. to Number

- 명시적 타입변환 : `Number()`을 사용
- 암묵적 타입변환

  > 특정 연산자들이 오는 `환경(문맥)`에서 일어난다. 그러한 환경에서는 항상 그 **표현식의 값이 숫자를 요구**하기 때문이다.

  - 비교연산자 : `>, <, <=, >=`
  - 비트연산자 : `|, &, ^, ~`
  - 산술연산자(+제외) : `-, *, /, %`
  - 단항연산자(unary operator) : `+`

    ```
    +3              //3
    +'3'            //3
    +false          //0
    +null           //0
    +undefined      //NaN
    +'javascript'   //NaN
    ```

  - `==` 연산자 : 위에서 `==`에서 같은 자료형으로 변형시킨후 비교한다고 말했다. 그 같은 자료형이 `number`이다. 즉, `==` 연산자에서의 문맥(context)는 숫자라고 할 수 있다.

    📌 `==` 연산자의 연산 방법

    1. 좌우 피연산자의 타입이 같을 때는 형변환이 일어나지 않고 비교한다.
    2. 한쪽 피연산자만 문자열이라면 그 문자열을 숫자로 변환 후 비교한다.
    3. 한쪽 피연산자가 객체라면 다른쪽 피연산자의 타입에 맞게 형변환하여 비교한다.(문자열 : 객체 => 문자열 / 숫자 : 객체 => 숫자)
    4. 한쪽 피연산자가 불리언이라면 불리언값을 숫자로 형변환하여 비교한다.

- 원시자료형 중에 숫자문자열의 경우엔 숫자로 바뀌는걸 쉽게 알수있다. 하지만 그 외의 자료형들은 어떤 숫자로 바뀌는지 알아야 형변환이 어떻게 진행될지를 예상할 수 있다. 원시자료형에 따른 숫자로의 형변환에 대해서 알아보자

  ```javascript
  Number(null); // 0
  Number(undefined); // NaN
  Number(''); // 0
  Number(true); // 1
  Number(false); //0
  Number('12'); //12
  Number('  12  '); //12
  Number('\n'); //0
  Number('12m'); //NaN
  ```

  > 숫자문자열은 숫자로 변환될 수 있다. 공백과 함께 있는 숫자문자열의 경우는 자바스크립트 엔진은 공백을 자동으로 제거한 후 형변환을 시킨다. 그렇기 때문에 문제없이 형변환이 일어날수있다.

  > 글자와 함께 있는 숫자는 NaN으로 변형된다. **NaN은 타입이 숫자**이다.

  > falsy value라고 알려진 `null, false, ''` 는 `0`으로 변환된다. 하지만 `undefined`는 `NaN`으로 바뀐다.

* null과 undefined의 예외적인 포인트

1. `==` 비교연산자를 사용하여 `null`와 `undefined`를 비교할 때는 **숫자로 형변환이 일어나지 않는다**. `null`과 `undefined`는 서로 간 혹은 같은 값끼리 비교할 때만 true가 되고 그 외의 것과 비교하면 `false`가 나온다.

   ```javascript
   null == null; //true
   null == undefined; //true
   undefined == undefined; //true
   null == 0; //false
   undefined == NaN; //false
   ```

   > 위에서 숫자형변환에 대한 내용을 생각해보면 `==`는 숫자로 형변환을 시킨 후 비교한다고 했다. 그리고 _`null`과 `undefined`는 `0`과 `NaN`으로 이러한 문맥에서는 형변환이 가능하다고 생각할 수 있다_. 하지만 결과값은 false라는 것을 볼 수 있다. 즉 **`==` 연산자를 사용할 때 `null`과 `undefined`는 형변환이 일어나지 않는다**.

2. `NaN`은 어느것과도 같지 않다. 심지어 자기자신과도 같지 않다.
   어떠한 비교연산자(== / ===)로 비교하던 `모두 false`이다.

📌 참고

```javascript
var a = '10';
var b = 5;
var result = a + b;
console.log(result); //105
console.log(typeof b, b); //number, 5
```

> 위의 변수 b의 값이 암묵적 타입 변환이 일어나서 문자열의 결합으로 `105`라는 결과가 나왔다. 이것을 보면 마치 b의 값이 문자열로 바껴서 재할당이 일어난 것으로 착각할 수 있다. 그것이 아니라 변수b를 바탕으로 '5'를 임시의 값으로서 생성하여 결과값을 출력한 뒤(표현식의 평가가 끝난 뒤) 어떠한 것도 이 임시 값을 참조하지않기 때문에 가비지 컬렉터에 의해서 사라지게 된다. 그래서 b의 값은 변함없이 `number타입의 5`라는 값을 갖는 것이다.

## 객체

> 객체가 변환될 때 가장 먼저 하는 일은 `원시자료형`으로 변형시키는 것이다. 그리고 나서 `문맥(context)`에 따라서 `숫자(number), 문자열(string), 불리언(boolean)`로 변형시킨다.

1. to Boolean

- 원시자료형이 아닌 자료형, 객체가 불리언으로 변형될 때는 객체가 어떤 값을 갖고있는지에 상관없이 무조건 `true`로 변형된다. So Simple 😎

2. to String / to Number

- 모든 객체는 `toString()` 과 `valueOf()`라는 메소드를 가지고 있다(상속받는 것). 이 두가지 메소드는 반드시 `원시자료형을 가진 값`을 반환한다. 만약 객체를 반환하면 그 값은 무시된다. 객체의 형변환은 위 두가지 메소드에 의해서 일어난다.

- 객체는 내부프로퍼티인 [[ToPrimitive]]에 따라서 어떤 원시자료형으로 변형할지를 결정한다. 그에 따라서
  `toString()`을 사용할지 `valueOf()`를 사용할지를 선택한다.

- 객체의 형변환

  > 객체는 대부분 문자열로 형변환이 되면 `"[object Object]"` 문자열을 반환한다.

  > 객체는 먼저 toString()에 의해서 문자열로 변환된다. 하지만 내부의 값이 나오는 것이 아니라 `"[object Object]"` 이렇게 값을 출력한다. 그 후에 문맥이 숫자를 요구하는 곳이라면 `"[object Object]"` 문자열을 숫자로 바꿔야하는데 바꿀수없는 것이기때문에 `NaN`이 나오게 된다.

  ```javascript
  String({}); //"[object Object]"
  String({ a: 1 }); //"[object Object]"
  Number({}); //NaN
  Number({ a: 1 }); //NaN
  ```

- 배열의 형변환

  > 배열도 객체지만 보여지는 현상이 약간 다르게 작동한다. 객체처럼 toString()이 작동하지만 마치 `Array메소드의 join()`처럼 작동한다. 그렇기때문에 배열 내부의 요소를 문자열로 반환한다. 그 후 숫자로 변형되야한다면 마찬가지로 문자열에서 숫자로 변형되는 형변환을 따른다.

  ```javascript
  String([]); //""
  String([1, 2, 3]); //"1,2,3"
  //[1,2,3].join()
  Number([]); //0
  Number([1, 2, 3]); //NaN
  ```

## Solution to preview

> 맨위의 preview 문제에 대한 풀이입니다.

```javascript
1. true + false             // 1
2. 12 / "6"                 // 2
3. "number" + 15 + 3        // 'number153'
4. 15 + 3 + "number"        // '18number'
5. [1] > null               // true
6. "foo" + +"bar"          // 'fooNaN'
7. 'true' == true           // false
8. false == 'false'         // false
9. null == ''               // false
10. !!"false" == !!"true"    // true
11. ['x'] == 'x'             // true
12. [] + null + 1            // 'null1'
13. [1,2,3] == [1,2,3]       // false
14. {}+[]+{}+[1]             // '0[object Object]1'
15. !+[]+[]+![]              // 'truefalse'
16. new Date(0) - 0          // 0
17. new Date(0) + 0          // 'Thu Jan 01 1970 09:00:00 GMT+0900 (대한민국 표준시)0'
```

1. **true + false**

```
문맥 - 숫자
true + false     : 불리언 => 숫자
1 + 0            : true => 1  / false => 0
1
```

2. **12 / "6"**

```
문맥 - 산술연산자 => 숫자
12 / "6"         : 숫자문자열 => 숫자
12 / 6
2
```

3. **"number" + 15 + 3**

```
문맥 - 피연산자 중에 문자열 존재 => +의 결합 / +연산 좌결합성
"number" + 15 + 3
"number15" + 3
"number153"
```

4. **15 + 3 + "number"**

```
문맥 - 첫번째 + 경우 숫자 / 두번째 + 경우 문자열존재 => 결합 / +연산 좌결합성
15 + 3 + "number
18 + "number"
"18number"
```

5. **[1] > null**

```
문맥 - 숫자
[1] > null      : 배열의 경우 배열 => 문자열 /  null은 falsy value로서 0으로 변환
"1" > 0         : 숫자문자열 => 숫자
1 > 0
true
```

6. **"foo" + +"bar"**

```
산술연산자인 + 보다 단항연산자의 + 가 연산자 우선순위가 높기 때문에 먼저 연산된다.
"foo" + +"bar"          : 문맥 - 단항연산자 + 는 숫자
"foo" + (+"bar")        :  +"bar" => NaN
"foo" + NaN             : 문맥 - 문자열
"fooNaN"
```

7. **'true' == true**

```
문맥 - 숫자
'true' == true          :  'true' => NaN / true => 1
NaN == 1
false
```

8. **false == 'false'**

```
문맥 - 숫자
false == 'false'        :  false => 0  / 'false' => NaN
0 == NaN
false
```

9. **null == ''**

```
문맥 - 숫자
null == ''              : '' => 0
null == 0               : null은 == 연산에서 형변환이 되지 않는다
false
```

10. **!!"false" == !!"true"**

```
문맥 - !! => 불리언 : 피연산자를 불리언으로 형변환
논리연산자가 == 동등연산자보다 연산자 우선순위가 높기 때문에 먼저 평가된다
!!"false" == !!"true"       : falsy value를 제외한 모든 값은 true이다
!!true == !!true            : 이중부정은 true이기 때문에 결국 true와 같다
true == true
true
```

11. **['x'] == 'x'**

```
(시작점) 문맥 - 숫자
['x'] == 'x'                : 배열의 경우 문자열로 먼저 형변환이 일어난다.
'x' == 'x'                  :  == 연산자는 피연산자가 같은 타입이면 형변환이 일어나지 않는다
true
```

12. **[] + null + 1**

```
(시작점) 문맥 : (문자열이 없는) + 연산을 하기위해선 모두 숫자로 형변환이 되야한다
+ 좌결합성
[] + null + 1           : [] => ''
'' +  null + 1          : 형변환과정 중에 문자열이 생성되어 +연산이 결합으로 바뀌었다
'null1'
```

13. **[1,2,3] == [1,2,3]**

```
[1,2,3] == [1,2,3] : 객체의 비교를 물어보는 문제로서 피연산자가 모두 타입이 같기 때문에 타입변환은 일어나지않는다.
이제 객체가 같은지를 비교하면 된다. 그런데 객체의 비교에서 중요한 것은 그 안의 값이 아니라 객체의 참조가 같은지이다.
하지만 여기서는 2개가 다른 객체 참조를 갖기때문에 false이다
false
```

14. **{}+[]+{}+[1]**

```
이 문제는 사실 이해하기 쉽지않았다. {}이 의미하는 바가 무엇인지 알지못했기 때문이다. {}이 의미하는 바는 2가지다.
첫번째는 객체 리터럴이고 두번째는 블럭문장이다. +연산에서 객체는 원시자료형으로 변환되는데,우선 문자열로 형변환되어 "[object Object]" 반환한다.
그렇다면 블럭문장은?? 기본적으로 문장(statement)는 값을 리턴하지 않는다. 하지만 +연산에서는 에러는 보내지 않는
대신 0을 암묵적으로 형변환하여 리턴한다.

console.log({ a : 1})  //{a: 1} 라는 객체 리턴
console.log({ const a = 1, function(){}}) //Uncaught SyntaxError: Unexpected identifier

두번째 코드가 에러가 나는 이유는 console.log는 문장을 인자로 받을 수 없기 때문이다.
즉 문장은 값을 낼 수 없기 때문에 콘솔에 찍을 수가 없는 상황이라 에러가 뜨는 것이다.

console.log({}) // {} 라는 빈객체 리턴

이 코드가 빈객체를 리턴하는 것을 이해할 수 있는가? {} 이것이 의미하는 것은 위에서 설명했듯이 2가지 가능성이 있다.
하지만 console.log에는 당연히 값이 나올 수 있는 표현식이 들어가야하기 때문에 {}을 당연히 객체리터럴의 표현으로 인식하는 것이다.

위 문제로 돌아가면 첫번째 {}는 여기서 블럭문장으로 인식하여 0을 반환한다.
하지만 두번째 {}는 객체리터럴로 인식하여 "[object Object]"을 반환한다. 왜 이렇게 인식할까?

여기서부터는 나의 추론...
+는 좌결합성이기 때문에 {} + []를 평가하게 된다. +연산은 기본적으로 숫자의 연산이기 때문에
문맥이 숫자인 상황에서 숫자를 리턴할 수 있는 형변환을 선택하게 된다. 그래서 0을 반환하는 블럭문장으로 {}를 인식하여 0을 리턴한다.
그 다음 []는 빈문자열을 반환한다. 이제 +연산에 피연산자가 문자열이 들어왔다. 즉 0과 ''의 결합이 된 것이다. 그렇게 첫번째 연산은 '0'이 되고
그 뒤의 {}는 문맥이 문자열이 되었기에 "[object Object]"를 리턴하게 된 것이라고 생각한다.

{}+[]+{}+[1]
0 + '' + "[object Object]" + "1"
"0[object Object]1"
```

15. **!+[]+[]+![]**

```
연산자 우선순위와 +의 좌결합성에 의해 연산순서가 정해진다
!+[]+[]+![]
(!+[]) + [] +(![])
: ()는 먼저 연산되는 것들 / 문맥 - 숫자 / [] => '' => 0 / !(논리연산자)에 의해서 불리언으로 형변환 - [] => true
(!0) + [] + !true       : !(논리연산자)에 의해서 불리언으로 형변환 - !0 => true
true + [] + false       : [] => ''
'true' + false          : +연산에서 문자열이 나타나서 결합이 된다
'truefalse'
```

16. **new Date(0) - 0**

```
문맥 - 숫자(-산술연산자)
new Date(0) - 0             : new Date(0) => 'Thu Jan 01 1970 09:00:00 GMT+0900 (대한민국 표준시)' => 0
0 - 0
0
```

17. **new Date(0) + 0**

```
(시작점) 문맥 - 숫자
new Date(0) + 0             : new Date(0) => 'Thu Jan 01 1970 09:00:00 GMT+0900 (대한민국 표준시)'
'Thu Jan 01 1970 09:00:00 GMT+0900 (대한민국 표준시)' + 0 : 문자열이 나타나서 결합이 된다
'Thu Jan 01 1970 09:00:00 GMT+0900 (대한민국 표준시)0'
```

# Ref

- [타입 변환과 단축 평가](https://poiemaweb.com/js-type-coercion)
- [JavaScript type coercion explained](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/)
- [객체를 원시형으로 변환하기](https://ko.javascript.info/object-toprimitive)
- [What you need to know about Javascript's Implicit Coercion 번역](https://velog.io/@jakeseo_me/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%9D%BC%EB%A9%B4-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%A0-33%EA%B0%80%EC%A7%80-%EA%B0%9C%EB%85%90-4-%EC%95%94%EB%AC%B5%EC%A0%81-%ED%83%80%EC%9E%85-%EB%B3%80%ED%99%98-%EB%B2%88%EC%97%AD)
