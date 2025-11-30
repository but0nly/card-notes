#vim

### 任务点

| 操作 | 键位 | 
| --- | --- | 
| 删除光标所在字符 | x |
| 删除光标前的字符 | X |
| 删除当前光标的字符并进入 insert 模式 | s |
| 删除当前光标所在行并进入 insert 模式 | S |
| 替换一个字符 | r | 
| 替换多个字符 | R |
| undo/redo 可撤销块(进入insert模式开始,直到返回normal模式为止,在此期间输入或删除的任何内容都被当作一次修改) | u |

### 练习

```js
function getUserName(){
  const name = "jone";
  return "John"
}
```