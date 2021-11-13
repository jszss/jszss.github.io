---
title: sql-updateDate
author: zss
date: 2021-10-20 15:56:49
tags: [sql]
---

```sql
  `createDate` datetime(6) NOT NULL DEFAULT CURRENT_TIMESTAMP(6) COMMENT '创建时间',
  `updateDate` datetime(6) NOT NULL DEFAULT CURRENT_TIMESTAMP(6) ON UPDATE CURRENT_TIMESTAMP(6) COMMENT '最后更新时间',
```
