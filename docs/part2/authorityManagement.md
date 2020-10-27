# 权限管理

本项目权限管理采用用户表，权限表，角色表分别进行管理。

## 权限表

项目所有权限如下，分为二级权限管理模式，其中一级权限用于侧边栏渲染对应组件，二级权限用于控制组件中相应功能，以达到不同权限用户生成不同页面及不同功能的作用。


<table>
	<tr>
        <td colspan="2">一级权限</td>
        <td colspan="2">二级权限</td>
    </tr>
	<tr>
        <td>权限名</td>
        <td>对应组件</td>
        <td>权限代码</td>
        <td>权限内容</td>
    </tr>
    <tr>
        <td rowspan="5">user</td>
        <td rowspan="5">
            AuthorityManagement/<br>UserManagement
        </td>
        <td>user:view</td>
        <td>查看用户</td>
    </tr>
    <tr>
        <td>user:add</td>
        <td>添加用户</td>
    </tr>
    <tr>
        <td>user:update</td>
        <td>修改用户</td>
    </tr>
    <tr>
        <td>user:delete</td>
        <td>删除用户</td>
    </tr>
    <tr>
        <td>user:assignRoles</td>
        <td>分配角色</td>
    </tr>
    <tr>
        <td rowspan="5">role</td>
        <td rowspan="5">
            AuthorityManagement/<br>RolerManagement
        </td>        
        <td>role:view</td>
        <td>查看角色</td>
    </tr>
    <tr>
        <td>role:add</td>
        <td>添加角色</td>
    </tr>
    <tr>
        <td>role:update</td>
        <td>修改角色</td>
    </tr> 
    <tr>
        <td>role:delete</td>
        <td>删除角色</td>
    </tr>
    <tr>
        <td>role:assignPowers</td>
        <td>分配权限</td>
    </tr>
    <tr>
        <td rowspan="4">power</td>
        <td rowspan="4">
            AuthorityManagement/<br>PowerrManagement
        </td>
        <td>power:view</td>
        <td>查看权限</td>
    </tr>
    <tr>
        <td>power:add</td>
        <td>添加权限</td>
    </tr>
    <tr>
        <td>power:update</td>
        <td>修改权限</td>
    </tr>
    <tr>
        <td>power:delete</td>
        <td>删除权限</td>
    </tr>
    <tr>
        <td>data</td>
        <td>DataOverView</td>
        <td>data:view</td>
        <td>数据总览</td>
    </tr> 
    <tr>
        <td>search</td>
        <td>Search</td>
        <td>search:view</td>
        <td>结节搜索</td>
    </tr>
    <tr>
        <td>case</td>
        <td>CaseManagement</td>
        <td>case:view</td>
        <td>病例展示</td>
    </tr>     
</table>


## 角色表

项目包含4类角色如下表所示。其中**普通标注者**仅有标注数据权限，**一级审核者**可审核普通标注者标注数据，**二级审核者**可对审核数据复核，**管理员**拥有全部权限，可管理其他账号。

| 角色名称   | 角色描述             | 权限                                                         |
| ---------- | -------------------- | ------------------------------------------------------------ |
| 管理员     | 拥有全部权限的管理员 | ['user:view','user:add','user:update','user:delete','user:assignRoles',<br>'role:view','role:add','role:update','role:delete','role:assignPowers', '<br>power:view', 'power:add', 'power:update', 'power:delete', <br>'data:view', 'search:view', 'case:view'] |
| 二级审核者 | 二次审核标注数据     | ....                                                         |
| 一级审核者 | 审核标注后数据       | ....                                                         |
| 标注者     | 只拥有标注数据的权限 | ....                                                         |

## 用户表

用户表中包含字段如下，其中**userID**作为在数据库中查询的唯一标识，**username**与**password**作为用户登录用户名与密码，**role**中为该用户对应角色。

| userID | username   | password(加密前) | role       |
| ------ | ---------- | ---------------- | ---------- |
| 001    | admin      | admin            | 管理员     |
| 002    | panzhen    | panzhen          | 标注者     |
| 003    | doctorwang | doctorwang       | 二级审核者 |



# 