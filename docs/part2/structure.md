# 项目组织结构

项目文件层次结构如下：

```
.
├── public              	#
│   ├── index.html          # The origin html
│   └── manifest.json       # 
│
├── src		                # main source file holder
│   ├── component           # React component library
│   ├── image               # Image file holder
│   ├── redux               # userInfo
│   ├── public              # 存放全局变量
│   ├── App.js				
│   ├── index.js
│   └── DashBoard.js        # 主文件
│
├── servers		            # 后端文件夹，包含后端api实现
├── ...                     
├── package.json            # Shared devDependencies and commands
└── README.md               # This file
```

React组件放于src/component中，每个组件形成文件夹，由index.js文件导出，引用时引用至文件夹即可，如：

```
import {CaseManager} from './component/CaseManagement';
```

