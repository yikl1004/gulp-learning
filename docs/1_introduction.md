## 1. 서론
### 1.1. 개요
> - 프로젝트에서 반복해서 수행하는 **빌드**, **테스트**, **배포** 등을 자동화해서 **하나의 명령어로 간단하게 실행할 수 있게 하는 도구** 인 gulp를 사용해본다.
> - gulp는 프론트엔드 개발에서 유용하게 쓰일 수 있는 모듈을 플러그인 형태로 제공 한다.  
> - 이 플러그인 들을 조합해 자신만의 개발환경을 구축해 볼 수 있고, 또 다양한 테스트와 실험이 가능하다.  
> - 최근 Node.js Foundation에서는 Node.js 에 ES6를 적용했다고 밝힌바 있다. 아직 완벽히 구현된 것은 아니지만 상당수 구현이 되어있어 Node.js 서버 사이드에서는 ES6문법을 사용할 수 있다.

### 1.2. 목적
> 기존의 에디터와 브라우저 만으로는 한계가 있었던 다양한 언어의 Framework들을 사용해보고 익혀 실제로 구현해 본다.
- **CSS** : SASS, LESS 등.
- **HTML** : Jade, Mustache, Handlebars... and React, Angular2
- **Javascript** : ES2015, Vanilla script... and Polyfill(for Cross Browsing)
- **TEST-DATA** : JSON, Deployd 구축

### 1.3. 구성원
| github ID    | 구성원 | 담당분야       | 비고        |
| ------------ |:------:|:--------------:|------------:|
| yikl1004     | 명기   | gulp packaging | Key Player  |
|              | 미경   |                | Advisor     |
|              | 희욱   |                | Player      |
|              | 현아   |                | Player      |

### 1.4. ES2015
> 이 프로젝트에서는 기본적인 문법으로 ES2015사용을 전제로 한다.  
> ES2015(이하 ES6)는 이미 표준으로 정의된 javascript 문법이다. 다음은 ES6의 장/단점이다.
- 장점
    - 즉시 실행 함수 없이 Block scope 생성이 가능하다.
    - 비동기 프로그래밍을 위한 Promise를 제공한다.
    - 헤체 할당, 전개 연산, 간단한 함수인 화살표 함수를 제공한다.
    - class 키워드를 통한 class를 생성할 수 있다. (기존 prototype 체이닝을 통한 다소 복잡한 패턴을 쓰지 않아도 class 사용 가능)
    - 함수단위보다 큰 개념인 모듈단위로 스코프를 관리할 수 있다.
- 단점
    - 현재 100% 지원되는 브라우저가 없다.
    - babel 이라는 compiler 없이 사용하기가 힘들다.
    - Cross Browsing 의 한계가 있다. 맞추려면 babel, babel-polyfill, es5-shim 같은 compiler와 polyfill 라이브러리의 사용이 필수 적이다. 이로 이한 퍼포먼스 문제도 함께 따른다.  

자세한 내용은 [es6-features](http://es6-features.org/#Constants)를 참조.

#### 1.4.1. 간략한 소개
##### 1. arrow function (화살표 함수)
```js
//ES5
function func( arg ) {
    console.log(arg)
}

//ES6

//case 1
const func = arg => console.log(arg)

//case 2
const function (arg) => {
    return console.log(arg);
}
```

##### 2. spread operator (전개 연산자)
```js
//ES5
var arr = [1, 2, 3];
for( var i=0; i<arr.length; i+=1 ) {
    console.log(arr[i]);
}

//ES6
const arr = [1, 2, 3];
console.log(...a);
```

##### 3. Destructuring assignment(해체 할당)
```js
//ES5
var obj = {
    a: 1,
    b: 2,
    c: 3
};

var a, b, c;
a = obj.a;
b = obj.b;
c = obj.c;

//ES6
const obj = {
    a: 1,
    b: 2,
    c: 3
};

const {a, b, c} = obj;
```
