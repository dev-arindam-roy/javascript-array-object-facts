# javascript Array & Object Debugging Facts
A snippet for javascript array and object debugging facts and outputs

```js

var x = [];
console.log(x); // []
console.log((x) ? true : false); // true
console.log(typeof x); // "object"
console.log(x.length); // 0
console.log(x[0]); // undefined
console.log((x[0]) ? true : false); // false

console.log(x[0] === undefined); // true
console.log(x[0] === 'undefined'); // false

console.log(x[0] == undefined); // true
console.log(x[0] == 'undefined'); // false

console.log(typeof x[0] === 'undefined'); // true
console.log(typeof x[0] == 'undefined'); // true
console.log(typeof x[0] === undefined); // false
console.log(typeof x[0] == undefined); // false

x = ['item1', 'item2', 'item3', 'item4'];
console.log(x); // ["item1", "item2", "item3", "item4"]
console.log(x.length); // 4
console.log(x[0]); // "item1"
console.log(x[x.length - 1]); // "item4"

x[4] = 'item5';
console.log(x); // ["item1", "item2", "item3", "item4", "item5"]

x[x.length] = 'item6'; // ["item1", "item2", "item3", "item4", "item5", "item6"]
console.log(x);

x[x.length] = [];
console.log(x); // ["item1", "item2", "item3", "item4", "item5", "item6", []]

x[x.length - 1][0] = 'sub-item1';
x[x.length - 1][1] = 'sub-item2';
console.log(x[x.length - 1]); // ["sub-item1", "sub-item1"]

console.log(x); // ["item1", "item2", "item3", "item4", "item5", "item6", ["sub-item1", "sub-item1"]]

x[x.length - 1].push('sub-item3');
x[x.length - 1].push('sub-item4');
console.log(x); // ["item1", "item2", "item3", "item4", "item5", "item6", ["sub-item1", "sub-item2", "sub-item3", "sub-item4"]]

x.push('item7');
x.push('item8');
console.log(x); // ["item1", "item2", "item3", "item4", "item5", "item6", ["sub-item1", "sub-item2", "sub-item3", "sub-item4"], "item7", "item8"]

console.log(x.toString()); // "item1,item2,item3,item4,item5,item6,sub-item1,sub-item2,sub-item3,sub-item4,item7,item8"

console.log(Array.isArray(x)); // true
console.log(typeof x); // "object"

console.log(JSON.stringify(x));
// "[\"item1\",\"item2\",\"item3\",\"item4\",\"item5\",\"item6\",[\"sub-item1\",\"sub-item2\",\"sub-item3\",\"sub-item4\"],\"item7\",\"item8\"]"

let newx = JSON.parse(JSON.stringify(x));
console.log(newx); // ["item1", "item2", "item3", "item4", "item5", "item6", ["sub-item1", "sub-item2", "sub-item3", "sub-item4"], "item7", "item8"]
console.log(Array.isArray(newx)); // true
console.log(typeof newx); // "object"

/** --------------------------------------------------- **/
/** javascript Array To Json Object Creation **/
/** --------------------------------------------------- **/

let newx2 = Object.assign({}, newx);
console.log(newx2);
/**
[object Object] {
  0: "item1",
  1: "item2",
  2: "item3",
  3: "item4",
  4: "item5",
  5: "item6",
  6: ["sub-item1", "sub-item2", "sub-item3", "sub-item4"],
  7: "item7",
  8: "item8"
}
**/
console.log(typeof newx2); // "object"
console.log(Array.isArray(newx2)); // false
console.log(newx2.length); // undefined

console.log(Object.keys(newx2)); // ["0", "1", "2", "3", "4", "5", "6", "7", "8"]
console.log(typeof Object.keys(newx2)); // "object"
console.log(Array.isArray(Object.keys(newx2))); // true
console.log(Object.keys(newx2).length); // 9

/** ---------------------------------------------------------------- **/
/** javascript Json Object To Array Creation **/
/** ---------------------------------------------------------------- **/

console.log(Object.values(newx2)); // ["item1", "item2", "item3", "item4", "item5", "item6", ["sub-item1", "sub-item2", "sub-item3", "sub-item4"], "item7", "item8"]
console.log(Object.values(newx2).length); // 9

/** ---------------------------------------------------------------- **/
/** javascript Json Object To Array (key, value) Creation **/
/** ---------------------------------------------------------------- **/

console.log(Object.entries(newx2));
/**
[["0", "item1"], ["1", "item2"], ["2", "item3"], ["3", "item4"], ["4", "item5"], ["5", "item6"], ["6", ["sub-item1", "sub-item2", "sub-item3", "sub-item4"]], ["7", "item7"], ["8", "item8"]]
**/
console.log(Object.entries(newx2).length); // 9

console.log(JSON.stringify(newx2));
/**
"{\"0\":\"item1\",\"1\":\"item2\",\"2\":\"item3\",\"3\":\"item4\",\"4\":\"item5\",\"5\":\"item6\",\"6\":[\"sub-item1\",\"sub-item2\",\"sub-item3\",\"sub-item4\"],\"7\":\"item7\",\"8\":\"item8\"}"
**/
console.log(typeof JSON.stringify(newx2)); // "string"
console.log(JSON.stringify(newx2).length); // 151


//console.log(JSON.parse(newx2)); // ERROR, as JSON.parse not working upon an object, it only work on json string
console.log(JSON.parse(JSON.stringify(newx2)));
/**
[object Object] {
  0: "item1",
  1: "item2",
  2: "item3",
  3: "item4",
  4: "item5",
  5: "item6",
  6: ["sub-item1", "sub-item2", "sub-item3", "sub-item4"],
  7: "item7",
  8: "item8"
}
**/

let newx3 = Object.entries(newx2);
let newx4 = Object.assign({}, newx3);
console.log(newx4);
/**
[object Object] {
  0: ["0", "item1"],
  1: ["1", "item2"],
  2: ["2", "item3"],
  3: ["3", "item4"],
  4: ["4", "item5"],
  5: ["5", "item6"],
  6: ["6", ["sub-item1", "sub-item2", "sub-item3", "sub-item4"]],
  7: ["7", "item7"],
  8: ["8", "item8"]
}
**/

console.log(newx[0]); // "item1" (get from array)
console.log(newx2[0]); // "item1" (get from json object)
console.log(newx3[0]); // ["0", "item1"] (get from array)
console.log(newx4[0]); // ["0", "item1"] (get from json object)

let newx3CreateArray = [];
if (newx3.length > 0) {
  newx3.forEach((item, index, arr) => {
    //console.log(index, item); // working expected
    let key = 'myArrayKey' + index; // don't use space or hyphane during variable creation
    newx3CreateArray.push({[key] : item});
  });
}
console.log(newx3CreateArray);
console.log(JSON.stringify(newx3CreateArray));
console.log(JSON.parse(JSON.stringify(newx3CreateArray)));
let newx10 = JSON.parse(JSON.stringify(newx3CreateArray));
console.log(newx10[0].myArrayKey0);
console.log(newx10[6].myArrayKey6);

```

> ** To manage the Json/Object/Array - need below codes**
```js

Array.isArray(arr); // to check array or not
JSON.stringify(arr); // to convert array to string
let obj = Object.assign({}, arr); // to convert array to json object
Object.keys(obj); // to get only keys of any objects in an array
Object.values(obj); // to get only values of any objects in an array
Object.entries(obj); // to create an array of array with object's each key and value
JSON.parse(obj); // to convert json string to json object

```
