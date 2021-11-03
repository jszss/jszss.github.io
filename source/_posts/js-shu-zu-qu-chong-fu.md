---
title: 'JS 数组去重复'
date: 2019-09-09 10:36:38
tags: []
published: true
hideInList: false
feature: 
---
1. 使用 set 
```
function uniquearray(array) { 
    let unique_array= Array.from(set(array)) 
		return unique_array; 
}
```
2. 使用 filter
```
function unque_array (arr) {
  let unique_array = arr.filter(function(elem, index, self) {
    return index == self.indexOf(elem);
  })
  return unique_array;
}
 console.log(unique_array(array_with_duplicates));
```
3. 使用 for 循环
```
Array dups_names = ['Ron', 'Pal', 'Fred', 'Rongo', 'Ron'];
function dups_array(dups_names) {
 let unique = {};
 names.forEach(function(i) {
    If (!unique[i]) {
      unique[i] = true;    }
  });
return Object.keys(unique);}   // Ron, Pal, Fred, Rongo
Dups_array(names);

```