# 3. Project 구성하기

## 3.1. Directory 구조
> Project를 구성하기에 앞서 우리는 develop 버전과 Production 버전을 나누어서 관리를 해야 한다.  
> gulp는 develop 버전의 파일들을 ``task`` 명령어들을 거쳐 Production 버전의 가공된 파일을 만들어 내기 때문이다.  
> 디렉토리구조는 어떻게 가져갈 것이며 여기서 지정한 경로명과 문서(html, js, css)등의 name이 개발에 넘겨졌을 떄도 쓰이기 때문에 초기 계획단계에서 충분한 논의와 협의가 필요하다.  

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
