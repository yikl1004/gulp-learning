# 사전준비사항

## 2.1. 설치가 필요한 것 들
> [node.js](https://nodejs.org/ko/) 만 설치하면 된다.

## 2.2. node package 설치하기
### 2.2.1 npm 기본 명령어
- `npm init` : npm에서 사용할 package.json 파일 생성
- `npm [i | install] [packge-name]` : 설치
- `-g | --global` : 전역 설치
- `-S | --save` : package.json의 **dependency** 에 추가 됨, 의존 모듈 설정
- `-D | --save-dev` : `-S`의 과정을 포함하고 package.json의 **devDependency** 에 추가 됨, 의존 모듈 설정

자세한 상세 스펙은 [docs.npmjs.com](https://docs.npmjs.com/) 에서 볼수 있다.

## 2.3. 설치 할 package들
해당 package를 클릭하면 관련사이트로 이동합니다.
- [require-new](https://www.npmjs.com/package/require-new) : require의 cache를 무시하고 항상 새로운 모듈로 불러온다.
- [gulp](https://github.com/gulpjs/gulp/tree/master/docs) : 프론트엔드 자동화도구
- [gulp-webserver](https://www.npmjs.com/package/gulp-webserver) : 간단한 방법으로 로컬서버를 만들어준다.
- [gulp-livereload](https://www.npmjs.com/package/gulp-livereload) : 저장 할때마다 브라우저 새로고침을 자동으로 해준다.
- [jade](https://pugjs.org/api/getting-started.html) : HTML Template, jade 2.0.0 이후 [pug](https://github.com/pugjs/pug#rename-from-jade) 로 변경됨
- [gulp-jade](https://www.npmjs.com/package/gulp-jade) : gulpfile.js 에서 jade를 설정하고 실행한다.
- [gulp-prettify](https://github.com/jonschlinkert/gulp-prettify) : HTML 보기좋게 만들어 준다.
- [gulp-sass](https://www.npmjs.com/package/gulp-sass) : node-sass를 기본 엔진으로 sass,scss 파일을 gulp task상에서 compile한다.
- [gulp-cssbeautify](https://www.npmjs.com/package/gulp-cssbeautify) : css를 보기좋게 만들어준다.
- [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer) : 표준화 되지 않은 css property에 browser에 맞는 prefix를 달아 추가해준다. (참고: [browser list](https://github.com/ai/browserslist#queries))
- [gulp-imagemin](https://www.npmjs.com/package/gulp-imagemin) : 이미지 압축도구
- [imagemin-pngquant](https://www.npmjs.com/package/imagemin-pngquant) : imagemin에 없는 png압축 도구
- [gulp-minify](https://www.npmjs.com/package/gulp-minify) : js 압축/난독화

한번에 설치하기( gulp, gulp-webserver는 global 설치 )
> 1. npm i gulp gulp-webserver -g  
> 2. npm i gulp require-new gulp-webserver gulp-livereload jade gulp-jade gulp-prettify gulp-sass gulp-cssbeautify gulp-autoprefixer gulp-imagemin imagemin-pngquant gulp-minify -D
