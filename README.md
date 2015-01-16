AngularJS-numbers-only directive
----------------------------------

Requirement: allow entering of numbers with one (and only one!) decimal point. 

Demo is available here: http://plnkr.co/edit/ma3JBv7sH10wNzl4yjff?p=preview

```
.directive("numbersOnly", function () {
    return {
        require: "ngModel",
        link: function (scope, element, attrs, modelCtrl) {
            modelCtrl.$parsers.push(function (inputValue) {
                if (inputValue === undefined) return "";

                var isValid = !isNaN(parseFloat(inputValue)) && isFinite(inputValue);
                var newValue = inputValue;

                if (!isValid) {
                    // remove the last character 
                    newValue = inputValue.length > 1 ? inputValue.substring(0, inputValue.length - 1) : undefined;
                    if (inputValue === ".") { newValue = inputValue; }
                }

                if (newValue != inputValue) {
                    modelCtrl.$setViewValue(newValue);
                    modelCtrl.$render();
                }

                return newValue;
            });
        }
    };
});
```
