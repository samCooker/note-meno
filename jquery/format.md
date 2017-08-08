# jquery替换

- 方法封装
```
/**
 * 替换html字符串中的{x},x为参数下标
 * 如：
 *      formatHtml('<div>{0},{1}</div>','p1','p2')    --->   <div>p1,p2</div>
 * @param source
 * @param params
 * @returns {*}
 */
$.format = function (source, params) {
    if (arguments.length == 1)
        return function () {
            var args = $.makeArray(arguments);
            args.unshift(source);
            return $.format.apply(this, args);
        };
    if (arguments.length > 2 && params.constructor != Array) {
        params = $.makeArray(arguments).slice(1);
    }
    if (params.constructor != Array) {
        params = [params];
    }
    $.each(params, function (i, n) {
        source = source.replace(new RegExp("\\{" + i + "\\}", "g"), n);
    });
    return source;
};
```

- 调用方法

    $.format(str, param1,param2,...)
```
var text = "a{0}b{0}c{1}d\nqq{0}";
var text2 = $.format(text, 1, 2);
alert(text2);

```
