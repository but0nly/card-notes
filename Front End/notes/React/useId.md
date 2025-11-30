服务端配合客户端使用，保证React `streaming renderer`（流式渲染）的ID保持一致。
### 基本用法
```js
import { useId } from "react";

const Index: React.FC<any> = () => {
  const id = useId();

  return <div id={id}>大家好，我是小杜杜，一起玩转Hooks吧！</div>;
};

export default Index;
```