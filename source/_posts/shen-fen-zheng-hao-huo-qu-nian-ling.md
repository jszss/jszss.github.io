---
title: '身份证号获取年龄'
date: 2019-09-19 10:22:02
tags: [JS,js utils]
published: true
hideInList: false
feature: 
---
## 扫描数据回填（比如使用扫描枪，高拍仪）
```
// 扫描之后返回数据arr
function scanBackfill(arr){
    // 需要扫描回填的表单
    if(arr.constructor === Array){
        if(arr.length > 0){
            // 添加行数
            for (var i = 0; i < arr.length - 1; i++) {
                addLine(); // 该方法就是新增一行空数据模板dom的
            }
            // 数据回填
            arr.forEach(function(item, index){
                for (var key in item) {
                    if (item.hasOwnProperty(key)) {
                        $(document).find("input[name='"+ key +"']").val(item[key]);
                    }
                }
            });
        }
    }
}
```
## 身份证号获取年龄
```
function getAge(identityCard) {
    var len = (identityCard + "").length;
    if (len == 0) {
        return '';
    } else {
        if ((len != 15) && (len != 18)) //身份证号码只能为15位或18位其它不合法
        {
            return '';
        }
    }
    var strBirthday = "";
    if (len == 18) //处理18位的身份证号码从号码中得到生日和性别代码
    {
        strBirthday = identityCard.substr(6, 4) + "/" + identityCard.substr(10, 2) + "/" + identityCard.substr(12, 2);
    }
    if (len == 15) {
        strBirthday = "19" + identityCard.substr(6, 2) + "/" + identityCard.substr(8, 2) + "/" + identityCard.substr(10, 2);
    }
    //时间字符串里，必须是“/”
    var birthDate = new Date(strBirthday);
    var nowDateTime = new Date();
    var age = nowDateTime.getFullYear() - birthDate.getFullYear();
    //再考虑月、天的因素;.getMonth()获取的是从0开始的，这里进行比较，不需要加1
    if (nowDateTime.getMonth() < birthDate.getMonth() || (nowDateTime.getMonth() == birthDate.getMonth() && nowDateTime.getDate() < birthDate.getDate())) {
        age--;
    }
    return age;
}
```
[qui表单相关操作方法](https://juejin.im/post/5d822d516fb9a06b297582f0)