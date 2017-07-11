---
layout: post
title: Angular 한글 오류 문제
---

### Angular 한글 오류 문제

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
