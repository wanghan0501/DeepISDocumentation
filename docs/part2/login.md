# 用户登录过程

本项目采用redux进行登录状态管理。

用户在登录界面输入信息后，系统查询**用户表**，用户名与密码匹配之后根据用户表中**角色**字段得到用户角色，后查询**角色表**得到用户权限。

登录成功后采用[redux-persist](https://www.npmjs.com/package/redux-persist)机制将**username**、**userID**、**role**、**powers**信息写入SessionStorage中，key值为"persist:root";

在DashBoard组件中，使用

```javascript
sessionStorage.getItem("persist:root");
```



得到用户信息，并传递给需要的组件。

