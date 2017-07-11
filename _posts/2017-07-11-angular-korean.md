---
layout: post
title: Angular 한글 오류 문제
---


**[https://www.pinomap.com](pinonmap.com) 의 개발기**

Angular 1.2 버전 이상을 쓰다보면 input 박스나 textarea의 입력값이 한글의 조합형 문자라는 특성때문에
ng-model 에서 한글이 완성되지 않은 형태로 저장되는 버그가 있는데
이때 app.js 에서 아래의 코드를 추가시켜주면 된다

```javascript
 app.config(["$provide", '$routeProvider', "$locationProvider",
    function($provide, $routeProvider, $locationProvider) {
    
    $provide.decorator('inputDirective', ["$delegate", "$log", function($delegate, $log) {
            var directive = $delegate[0];
            angular.extend(directive.link, {
                post: function(scope, element, attr, ctrls) {
                    element.on('compositionupdate', function(event) {
                        element.triggerHandler('compositionend');
                        // e.stopImmediatePropagation();
                    })
                }
            });
            return $delegate;
        }]);
        $provide.decorator('textareaDirective', ["$delegate", "$log", function($delegate, $log) {
            //$log.debug('Hijacking input directive');
            var directive = $delegate[0];
            angular.extend(directive.link, {
                post: function(scope, element, attr, ctrls) {
                    element.on('compositionupdate', function(event) {
                        element.triggerHandler('compositionend');
                    })
                }
            });
            return $delegate;
        }]);
    
}]);

```
