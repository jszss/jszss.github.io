---
title: '实现前后端键名不一致的数据交换'
date: 2020-07-16 14:11:23
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
```js
//后台数据的模拟：
    let dataList = [
        {id: '1', name: '小狗', age: 5},
        {id: '2', name: '小羊', age: 8},
        {id: '3', name: '小猪', age: 10},
        {id: '4', name: '小牛', age: 12}
    ];
    //前台数据的模拟：
    let myList = [
        {myId: '1001', age: 18, myName: '张三'},
        {myId: '1001', age: 18, myName: '李四'}
    ];
    //数据中，数据的属性名称不同。

    //1.声明两个数组： 要求两个数组中的属性，一一对应；
    let myArr = ['myId', 'age', 'myName'];
    let dataArr = ['id', 'age', 'name'];
    // 2.调用适配函数，进行数据的转换；
    // console.log('没有转换的前台的数据:',myList);
    let data = myDataAdaptor(myList, dataList, myArr, dataArr);
    // console.log('转换后的前台的数据:',data);
    // 3. 自己页面逻辑中，如渲染一个table。

//封装的适配函数：
    function myDataAdaptor(myList, dataList, myArr, dataArr) {
        let newList = [];  //存储函数转换后的数据
//每循环一次，把后台数组中，一个对象中的指定的属性的值，赋值给前台模拟数据中对象指定的属性。
        for (let i = 0; i < dataList.length; i++) {
            let tempObj = dataList[i]; //后台返回的某一条数据，{id: '1', name: '肖明亚', age: 28}；
            let newObj = {};//一定是一个新的空对象。
            let j = 0;
            //for--in循环完成后，就把后台的一个对象的数据，变成前台的对象数据
            for (let key in tempObj) {
                // myArr[j] 去换 myArr数组中的值； j是0时， 'myId'
                // dataArr[j] 去换 dataArr数组中的值；j是0时， 'id'
                // 这儿实现对象数据的转换；
                newObj[   myArr[j]  ] = tempObj[  dataArr[j]  ]
                // newObj[  'myId' ] = tempObj[  'id'  ]
                // newObj.myId = 1;
/*
                 拿对象中的属性名：
                let q = myArr[j];  //'myId', 'age', 'myName'
                let h = dataArr[j];// 'id', 'age', 'name'
                newObj[q] = tempObj[h]
                j=0  newObj['myId'] = tempObj['id']
                j=1  newObj['age'] = tempObj['age']
                j=2  newObj['myName'] = tempObj['name']
*/
                j++;
            }
            newList.push(newObj)
        }
        return newList;
    }
————————————————
版权声明：本文为CSDN博主「李@@」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_44571638/java/article/details/107007629
```