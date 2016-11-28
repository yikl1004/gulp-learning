# 2. 사전준비사항

## 2.1. 설치가 필요한 것 들
> 1. [node.js](https://nodejs.org/ko/) 설치가 필요하다.  
> 2. 아래에서 소개할 gulp-livereload를 사용하기 위해서는 [Livereload](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei?hl=ko&utm_source=chrome-ntp-launcher) Chrome Extension을 설치해야 한다.

## 2.2. node package 설치하기
### 2.2.1. npm 기본 명령어

#### 설치하기에 앞서 기본 명령어를 알아본다.  

| command | explain |
|:-------:|:-------- |
| `npm init` | npm에서 사용할 package.json 파일 생성 |
| `npm install <packge-name>` | package 설치, `npm i <package-name>` 로 축약 가능 |
| `--global` | 전역 설치, `-g` 로 축약 가능 |
| `--save` | package.json의 dependency 에 추가 되면 의존 모듈을 설정한다, `-S` 로 축약 가능 |
| `--save-dev` | `--save`의 과정을 포함하고 package.json의 devDependency 에 추가 되며 의존 모듈을 설정한다, `-D` 로 축약 가능 |

자세한 spec은 [docs.npmjs.com](https://docs.npmjs.com/) 에서 볼수 있다.

## 2.3. 설치 할 package들
#### 해당 package를 클릭하면 관련사이트로 이동합니다.  

| package name | explain |
|:-------------|:--------|
| [require-new](https://www.npmjs.com/package/require-new) | require의 cache를 무시하고 항상 새로운 모듈로 불러온다.|
| [gulp](https://github.com/gulpjs/gulp/tree/master/docs) | 프론트엔드 자동화도구 |
| [gulp-webserver](https://www.npmjs.com/package/gulp-webserver) | 간단한 방법으로 로컬서버를 만들어준다. |
| [gulp-livereload](https://www.npmjs.com/package/gulp-livereload) | 저장 할때마다 브라우저 새로고침을 자동으로 해준다. |
| [jade](https://pugjs.org/api/getting-started.html) | HTML Template, jade 2.0.0 이후 [pug](https://github.com/pugjs/pug#rename-from-jade) 로 변경됨 |
| [gulp-jade](https://www.npmjs.com/package/gulp-jade) | gulpfile.js 에서 jade를 설정하고 실행한다. |
| [gulp-prettify](https://github.com/jonschlinkert/gulp-prettify) | HTML indent를 보기좋게 만들어 준다. |
| [gulp-sass](https://www.npmjs.com/package/gulp-sass) | node-sass를 기본 엔진으로 sass,scss 파일을 gulp task상에서 compile한다. |
| [gulp-cssbeautify](https://www.npmjs.com/package/gulp-cssbeautify) | css를 보기좋게 만들어준다. |
| [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer) | 표준화 되지 않은 css property에 browser에 맞는 prefix를 달아 추가해준다. (참고: [browser list](https://github.com/ai/browserslist#queries)) |
| [gulp-imagemin](https://www.npmjs.com/package/gulp-imagemin) | 이미지 압축도구 |
| [imagemin-pngquant](https://www.npmjs.com/package/imagemin-pngquant) | imagemin에 없는 png압축 도구 |
| [gulp-minify](https://www.npmjs.com/package/gulp-minify) | js 압축/난독화 |

한번에 설치하기( gulp, gulp-webserver는 global 설치 )
> 1. npm i gulp gulp-webserver -g  
> 2. npm i gulp require-new gulp-webserver gulp-livereload jade gulp-jade gulp-prettify gulp-sass gulp-cssbeautify gulp-autoprefixer gulp-imagemin imagemin-pngquant gulp-minify -D

## 2.4. Project 구성하기 전 해야 할일

### 2.4.1. gulpfile.js 작성
> gulp는 gulpfile.js 의 내용을 기준으로 해당되는 source들을 컴파일 하고 변동사항을 catch하여 re-compile이 가능하다.  
> 그리고 기존 자바스크립트의 문법을 그대로 따르며 node 최신버전 에서는 ES6를 99% 지원하고 있어 훨씬더 구조적이고, 간결한 프로그래밍을 할 수 있다.

#### 처음으로 해야 할 일은 필요한 의존 모듈을 commonJS 방식으로 불러오는 것 부터 시작한다.
```js
// 예시
const
	requireNew    = require('require-new'),
	gulp          = require('gulp'),
	webserver     = require('gulp-webserver'),
	livereload    = require('gulp-livereload'),
	realJade      = require('jade'),
	jade          = require('gulp-jade'),
	htmlbeauty    = require('gulp-prettify'),
	sass          = require('gulp-sass'),
	cssbeauty     = require('gulp-cssbeautify'),
	autoprefixer  = require('gulp-autoprefixer'),
	imagemin      = require('gulp-imagemin'),
	pngquant      = require('imagemin-pngquant'),
	jsmin         = require('gulp-minify');
```

#### 두번째로 문서내에서 사용될 파일경로, 각 모듈의 옵션, 실행 순서 등을 미리 정의해 둔다.
```js
const playTool = ['sass', 'jade', 'img', 'jsminify'],	//server 실행전 선행 작업
    // 기본경로
	defaultPath = {
		dest: 'front',
		src: 'front_src'
	},

    // src 경로
	path = {
		html: defaultPath.src + '/html/',
		css: defaultPath.src + '/com/css/',
		js: defaultPath.src + '/com/js/',
		img: defaultPath.src + '/img/'
	},

    // dest 경로
	outputPath = {
		html: defaultPath.dest + '/html/',
		css: defaultPath.dest + '/com/css/',
		js: defaultPath.dest + '/com/js/',
		img: defaultPath.dest + '/img/'
	},

    // 각 모듈의 옵션들...
	options = {
        // gulp-webserver
		server: {
            port: 8000,
            livereload: true,
            open: outputPath.html + 'index_detail.html'
        },

        // gulp-jade
		html: {
            indent_size: 4,
            indent_inner_html: true,
            unformatted: []
        },

        // gulp-cssbeautify
		css: {
            autosemicolon: true
        },

        //
		autoprefixer: {
			browsers: ['> 0%'],
			cascade: false
		},
		img: {
			optimizationLevel: 5,
            progressive: true,
            interlaced: true
		}
	};
```
이렇게 정의된 내용은 `task` 가 추가 되면서 사용 될 것이다.

### 2.4.2 Local server
gulp-webserver 를 이용하여 서버를 구동한다.

```js
//서버 시작
gulp.task( 'webserver', _ =>
	gulp.src( './' ).pipe( webserver( options.server ) )
);
```
