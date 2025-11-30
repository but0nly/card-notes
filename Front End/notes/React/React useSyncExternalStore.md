作用是外接第三方状态管理，例如 `redux`、`mobx`, 为了解决并发模式可能会出现状态不一致的问题。

### 基本用法
```js
import { useSyncExternalStore } from "react";
import { Button } from "antd";
import { combineReducers, createStore } from "redux";

const reducer = (state: number = 1, action: any) => {
  switch (action.type) {
    case "ADD":
      return state + 1;
    case "DEL":
      return state - 1;
    default:
      return state;
  }
};

/* 注册reducer,并创建store */
const rootReducer = combineReducers({ count: reducer });
const store = createStore(rootReducer, { count: 1 });

const Index: React.FC<any> = () => {
  //订阅
  const state = useSyncExternalStore(
    store.subscribe,
    () => store.getState().count
  );

  return (
    <>
      <div>大家好，我是小杜杜，一起玩转Hooks吧！</div>
      <div>数据源： {state}</div>
      <Button type="primary" onClick={() => store.dispatch({ type: "ADD" })}>
        加1
      </Button>
      <Button
        style={{ marginLeft: 8 }}
        onClick={() => store.dispatch({ type: "DEL" })}
      >
        减1
      </Button>
    </>
  );
};

export default Index;
```