# 3. Project 구성하기

## 3.1. Directory 구조
> Project를 구성하기에 앞서 우리는 develop 버전과 Production 버전을 나누어서 관리를 해야 한다.  
> gulp는 develop 버전의 파일들을 ``task`` 명령어들을 거쳐 Production 버전의 가공된 파일을 만들어 낸다. 이 가공된 파일은 개발단계에서 수없이 compiling 되어 계속 삭제와 생성을 반복하게 된다. 이 과정 때문에 build 된 파일은 직접 수정하여도 소용이 없다.
> 디렉토리구조는 어떻게 가져갈 것이며 여기서 지정한 경로명과 문서(html, js, css)등의 name이 개발에 넘겨졌을 떄도 쓰이기 때문에 초기 계획단계에서 충분한 논의와 협의가 필요했다.  

**root directory**  
![전체 디렉토리 이미지](https://github.com/yikl1004/gulp-learning/blob/master/img/example_diretory.png?raw=true)
- front : build된 파일들이 저장될 공간
- front_src : compile 되기 전 파일 이 저장될 공간 ( 주 작업 공간 )
- node_modules : node package 저장 공간
- gulpfile.js : gulp를 실행하기위한 task, config 집합 파일
- package.json : npm intializing file

**src directory**  
![src 디렉토리](https://github.com/yikl1004/gulp-learning/blob/master/img/example_sub_directory.png?raw=true)
- com : 공통된 source를 저장, 여기서는 css / j 를 포함하고 있음
- html : HTM 문서 저장, 하위경로가 필요할 경우 추가시켜 작업
- img : image file들을 저장
- inc : html include 를 위한 파일 저장, (태그 뿐만 아니라 가상으로 사용되는 데이터도 포함)

## 3.2 가상 data 준비하기
> 초기 계획단계에서 JSON으로 호출하여 Parsing하려 했으나 JADE에서 사용상에 한계가 있었다.  
> `JSON.parse`가 jade상에서 오류를 일으키는 문제인데 아직 까지도 정확한 원인분석은 하지 못했다. 당초 계획에선 임의의 가상 데이터를 만들어 실제로 데이터를 뿌려보는 것까지가 목표였으나 앞서 설명한 이유로 인하여 가상 데이터는 직접 하나하나 js in JADE 로 코딩하였다.  
> 이것을 조금더 쉬운 방법으로 Deployd 를 이용한 mongo db 를 생성하여 직접받아오는 방식으로 처리하려 했으나 다뤄지는 내용이 너무 방대해지는듯 하여 직접 데이터를 만드는 선에서 마무리 지었다.

아래 코드는 /front_src/inc/main-data.jade 내용의 일부를 발췌한 것이다.
```js
var jsonData = function(){
        return devDir.replace(/[']/gi, "");
    },
    gitPath = jsonData(),
    siteTitle = gitPath + '아모레퍼시픽 - 뷰티스퀘어',
    defaultPath = gitPath + '/front/com/',
    path = {css: defaultPath + 'css', js: defaultPath + 'js', img: gitPath + '/front/img/', html: gitPath + '/front/html/'},
    loadSource = {
        css: ['reset', 'beautysquare', 'plugins/swiper']
    },
    //- 네비게이션 ( gnb )
    menu = ['HOME', '뷰티뉴스', '제품도서관', '세일즈팁', '카운셀러톡', '라이프'],

    //- 메인비주얼 이미지
    mv_images = ['slide01', 'slide01', 'slide01', 'slide01', 'slide01'],

    latest_prod = {
        img: ['prod01', 'prod02', 'prod01', 'prod02', 'prod01'],
        tag: ['[헤라]', '[설화수]', '[헤라]', '[설화수]', '[헤라]'],
        title: [
            '화이트 프로그램 바이오 제닉이펙터',
            '자정미백 에센스',
            '화이트 프로그램 바이오 제닉이펙터',
            '자정미백 에센스',
            '화이트 프로그램 바이오 제닉이펙터'
        ]
    }
    ...
```
이러한 방식으로 가상의 데이터를 직접 코딩하여 jade에서 사용하였다.

## 3.3. 공통내용 분류
> inc 폴더에 포함될 파일들을 어떠한 기준으로 나눌 것인가를 생각해 보았지만 마땅히 획기적인 방법은 떠오르지 않았다.  
> 가장 간단하게 생각해 볼수 있는 단위인 language별로 나누기로 정하고, html에서 재사용 빈도가 높은 것은 따로 inc폴더에 파일을 생성하여 작업하였다.

아래는 예시 내용이다.
```js
// /front_src/inc/head.jade 의 내용
head
	//- base(href='http://yikl1004.github.io/bangpan')
	meta(charset='UTF-8')
	meta(name='robots', content='noindex, nofollow')
	meta(http-equiv='pragma', content='no-cache')
	meta(http-equiv='cache-control', content='no-cache')
	meta(http-equiv='Expires', content='-1')
	meta(http-equiv='Pragma', content='no-store')
	meta(name='format-detection', content='telephone=no')
	meta(name='viewport', content='width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no')
	script.
		//- //window.location.href = 'toapp:appviewchange:detailview:제품정보:/front/front/beautynews/main.do';
	title #{siteTitle} | #{subTitle}
	link(rel='stylesheet', type='text/css', href='#{path.css}/font.css')
	link(rel='stylesheet', type='text/css', href='#{path.css}/reset.css')
	link(rel='stylesheet', type='text/css', href='#{path.css}/beautysquare.css')
	link(rel='stylesheet', type='text/css', href='#{path.css}/plugins/swiper.css')
```

## 3.4. task 작성

### JADE
```js
// 제이드 템플릿
.task( 'jade', () => {

	// dev 경로의 설정을 JSON으로 받아 온다.
	options.html.data =  requireNew( './front_src/git.json' );
	// 받아온 결과 확인
	console.log('================',options.html.data);

	// task
	gulp.src( [`${path.html}*.jade`, `${path.html}**/*.jade`] )

        // jade 컴파일러
		.pipe( jade( options.html )
            // 에러 발생시 cli 코드 출력
	    	.on('error', (err) => {
				console.log(err);
			})
		)

        // html 정렬
		.pipe( htmlbeauty( options.html ) )

        // dest 파일 저장
		.pipe( gulp.dest( outputPath.html ) );

	console.log('JADE 실행 완료');
})
```
jade 실행 후 이어서 htmlbeautyfy를 실행한다.


### SCSS
```js
//scss 변환
.task( 'sass', () => {

    // src 경로와 build 파일 경로
	const compilePath = [ `${path.css}*.scss`, `${path.css}plugins/*.scss` ],
		  destPath = [outputPath.css, `${outputPath.css}plugins/`];

    //경로의 배열 length에 따른 순회 실행
    compilePath.map((elem, index) => {
        gulp.src( elem )

            // scss 컴파일 및 error 발생시 코드 출력
            .pipe( sass().on('error', sass.logError) )

            // 설정값에 따른 vendor prefix 자동 삽입
            .pipe( autoprefixer( options.autoprefixer ) )

            // css 정렬
            .pipe( cssbeauty( options.css ) )

            // 파일 저장
    		.pipe( gulp.dest( destPath[index] ) );    
    });
	console.log('SCSS 실행');
})
```
미리 src경로와 dest경로를 잡아 놓고 배열 API인 map을 돌려 배열의 length 만큼 실행 시킨다.

### Images
```js
//이미지 변환
.task('img', () => {
    return gulp.src(`./${path.img}**`)
        .pipe(imagemin( options.img ))
        .pipe(gulp.dest(`./${outputPath.img}`));
})
```
옵션 할당은 미리정의한 객체에서 가져온다.

### Watch
```js
// 항상 주시하기
.task( 'watch', ['webserver'], () => {
	// gulp.watch( `${defaultPath.dest}/git.json`, ['jade', 'sass'] );

	// html 감시
	gulp.watch( `${path.html}*.*`, ['jade'] );
	gulp.watch( `${path.html}**/*.*`, ['jade'] );

	// css 감시
	gulp.watch( `${path.css}*.*`, ['sass'] );
	gulp.watch( `${defaultPath.src}/inc/*.jade`, ['jade']);

	// 변화가 감지 될 시 브라우저 새로고침 실행
	livereload.changed( `${defaultPath.src}/**` );
})
```
watch를 사용하고 있는 경로마다 재실행 task를 배열로 지정할수 있다.  
livereload는 changed 메서드를 통해 브라우저 새로고침이 가능하고 위의 경로처럼 바꿔 놓으면 하위 파일이 어떤파일이든 변경되는 즉시 브라우저는 새로고침을 한다.
