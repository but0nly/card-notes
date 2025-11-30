#面试题 


```js

function isObject(obj) {
  return (typeof obj === 'object' && obj !== null)
}

function isEqual(obj1, obj2) {
  // 基础类型之间对比值
  if (!isObject(obj1) || !isObject(obj2)) {
    return obj1 === obj2
  }

  // 对比内存地址
  if (obj1 === obj2) {
    return true
  }


  const obj1Keys = Object.keys(obj1)
  const obj2Keys = Object.keys(obj2)

  // 对比字段和索引长度
  if (obj1Keys.length !== obj2Keys.length) {
    return false
  }


  // 递归对比
  for (const key in obj1) {
    if (Object.hasOwnProperty.call(obj1, key)) {

      const res = isEqual(obj1[key], obj2[key]);
      if (!res) {
        return false
      }
    }
  }

  return false
}

const o = { a: 'a' };
const o1 = o

console.log(isEqual(o, o1)) // true

console.log(isEqual({ a: '1' }, { a: '1' })) // false


```