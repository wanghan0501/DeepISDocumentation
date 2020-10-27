# 组件

React组件放于src/component中，每个组件形成文件夹，由index.js文件导出，主组件名与文件夹名相同。

组件css样式代码保存于同名.css文件中，如：

```
DataOverView.js
DataOverView.css
```

为适应redux要求，所有组件尽量写为function形式，而非class形式；在需使用生命周期等class功能时除外。

