---
title: 'jQ serializeJSON 表单格式化，支持数组'
date: 2019-12-19 08:50:16
tags: [表单]
published: true
hideInList: false
feature: 
---
```js
jQuery.fn.serializeJSON = function () {
    var json = {};
    jQuery.map(jQuery(this).serializeArray(), function (n, i) {
        var _ = n.name.indexOf('[');
        if (_ > -1) {
            var o = json;
            _name = n.name.replace(/\]/gi, '').split('[');
            for (var i = 0, len = _name.length; i < len; i++) {
                if (i == len - 1) {
                    if (o[_name[i]]) {
                        if (typeof o[_name[i]] == 'string') {
                            o[_name[i]] = [o[_name[i]]];
                        }
                        o[_name[i]].push(n.value);
                    }
                    else o[_name[i]] = n.value || '';
                }
                else o = o[_name[i]] = o[_name[i]] || {};
            }
        }
        else {
            if (json[n.name] !== undefined) {
                if (!json[n.name].push) {
                    json[n.name] = [json[n.name]];
                }
                json[n.name].push(n.value || '');
            }
            else json[n.name] = n.value || '';
        }
    });
    return json;
};
```