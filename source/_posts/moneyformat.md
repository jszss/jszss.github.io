---
title: 'MoneyFormat'
date: 2020-07-28 09:55:13
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
## 金额格式化
```js
      var money = 1200;
      var MoneyFormat = (money) => {
        const moneyStr = money.toLocaleString("en-IN", {
          style: "currency",
          currency: "CNY",
          currencyDisplay: "symbol",
          minimumFractionDigits: 2,
        })
        console.log("MoneyFormat -> moneyStr", moneyStr)
        return moneyStr.replace('CN','')
      };
      console.log(MoneyFormat(money)); ￥1,200.00
```