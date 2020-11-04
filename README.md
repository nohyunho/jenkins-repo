# DoDT Approval Plugin

## Install Node.js and Gulp 
 - 개발 환경에 Node.js v4.0.0+ 을 설치합니다.
 - Gulp를 global 옵션을 주어 설치합니다.
  
```sh
$ npm install --global gulp
```

## Add initial NPM packages
빌드에 필요한 NPM 패키지를 설치합니다.

```sh
$ npm install --save-dev gulp @jenkins-cd/js-builder
$ npm install --save @jenkins-cd/js-modules handlebars@3 
$ npm install --save datatables.net datatables.net-buttons 
$ npm install --save jszip pdfmake svg-to-pdfkit
$ npm install --save axios bootstrap-detached moment
```

## Add Javascript / CSS
자바스크립트 파일을 .jelly 파일에 추가하려면
 - gulpfile.js에 Bundle 생성목록을 추가합니다.
  .  js : builder.bundle('src/main/js/landingPage.js');
  . css : builder.bundle('src/main/css/navmenu/bootstrap.css');
  
 - Bundle 빌드를 위해 다음을 수행합니다.
 ```sh
$ gulp
```

 - jelly 파일에서 아래와 같이 Bundle을 로드합니다.
  .  js : <st:adjunct includes="org.jenkins.ui.jsmodules.approval-plugin.landingPage"/>
  . css : <st:adjunct includes="org.jenkins.ui.jsmodules.navmenu.bootstrap"/>
  
## Jenkins 실행
 - Local Jenkins 수행 : 
```sh
$ hpi:run -Djetty.port=8090
```
 - hpi Package 생성 : 
```sh
$ hpi:hpi
```

※서버에서 수행하려면 ${Jenkins_Home}/plugins 경로에 ${plugin_name}.hpi 파일을 위치시킨 후 재기동하면 됩니다.
