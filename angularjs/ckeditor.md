# CKeditor

```
https://github.com/lemonde/angular-ckeditor
npm install --save angular-ckeditor

=========================================
https://medium.com/bitmaker-software/scaffolding-a-new-angularjs-project-db01151f16e0
npm install -g yo gulp bower
npm install -g generator-gulp-angular
yo gulp-angular

bower install angular-ckeditor
bower install angular-ckeditor --save

=====================================
ckeditor version 4

bower install ckeditor
bower install ckeditor --save
bower install ckeditor#full/4.12.x --save

https://github.com/lemonde/angular-ckeditor
bower install angular-ckeditor
bower install angular-ckeditor --save

bower install ckeditor-youtube-plugin --save

js:
$scope.ckOptions = {
  language: 'en',
  allowedContent: true,
  extraPlugins: '',
  removeButtons: 'Save,NewPage',
  forcePasteAsPlainText: true
};

CKEDITOR.plugins.addExternal('youtube', '../ckeditor-youtube-plugin/youtube/');
$scope.ckOptions.extraPlugins = "youtube"

$scope.onCkReady = function() {
  console.log("ck ready");
}

$scope.onCkChange = function() {
  console.log("ck change");
  console.log($scope.content);
}

html:
  <div ckeditor="ckOptions" ng-model="content" ready="onCkReady()" ng-change="onCkChange()"></div>

```
