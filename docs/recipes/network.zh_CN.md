# console 录制和播放

从v0.9.15的下一个版本开始，我们增加了录制和播放fetch/ajax输出的功能。这个功能旨在为开发者提供更多的bug信息。对这项功能我们还提供了一些设置选项。

### 开启录制network功能
可以通过如下代码使用默认的配置选项
```js
rrweb.record({
  emit: emit(event) {
    // 如果要使用console来输出信息，请使用如下的写法
    const defaultLog = console.log["__rrweb_original__"]?console.log["__rrweb_original__"]:console.log;
    defaultLog(event);
  },
  // 使用默认的配置选项
  recordNetwork: true,
});
```

**警告**: 在emit函数中你不应该直接调用console.log等函数，否则将会得到报错：`Uncaught RangeError: Maximum call stack size exceeded`。
你应该调用console.log.\_\_rrweb_original__()来避免错误。


## 播放network数据
如果replayer传入的events中包含了network类型的数据，我们将自动播放这些数据。

```js
const replayer = new rrweb.Replayer(events, {
  networkConfig: (data)=>{
      console.log(data)
  },
});
replayer.play();
```
