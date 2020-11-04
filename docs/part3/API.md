[TOC]

# 前后端API定义

## 说明
本文档是智能肠胃组前端和后端之间数据接口的定义。文档中提供的方法名为系统前端接口的名称，供后端系统编写人员参考。以get开头的函数名表示该函数使用HTTP GET方法。接口返回值一律使用JSON格式的数据。接口暂时省略访问信息时的身份验证过程。每个代码片中展示了该接口的一个示例，传入参数和期望的返回值之间用空行分隔。示例只展示请求成功应该返回的结果；如果请求失败，要求返回404状态码。
## 用户信息接口
### 登录验证
|  方法名  |                loginValidation                 |
| :------: | :--------------------------------------------: |
| 传入参数 |        用户在登录表单输入的用户名和密码        |
|  返回值  | 如果数据库中存在匹配的用户名和密码返回用户信息 |

```javascript
POST /users/login
{
    username: "qin",
    password: "111" /* 待加密 */
}

{
    userId: 007,
    username: "qin",
    password: "111", /* 待加密 */
    roles: [roleId1, roleId2, ...],
}
```

### 获取单个用户信息
|  方法名  |         getUserInfo          |
| :------: | :--------------------------: |
| 传入参数 |            用户id            |
|  返回值  | 与该用户id匹配的用户全部信息 |

```javascript
GET /users/{userId}

{
    userId: 001,
    username: "admin",
    password: "admin",
    roles: [roleId1, roleId2, ...],
}
```

### 获取全部用户信息

|  方法名  |        getAllUsersInfo         |
| :------: | :----------------------------: |
| 传入参数 |               -                |
|  返回值  | 一个包含系统所有用户信息的列表 |

```javascript
GET /users

[
    {
        userID: 001,
        username: "admin",
        password: "admin",
        roles: [roleId1, roleId2, ...]
    },
    ...
]
```

### 添加用户信息
|  方法名  |        addUser        |
| :------: | :-------------------------: |
| 传入参数 | 待添加的用户名，密码，角色信息 |
|  返回值  | 用户信息是否添加成功  |

```javascript
POST /users
{
    username: "qin", 
    password: "111",
    roles: [roleId1, roleId2, ...]
}

Status: 200
```

### 更新用户信息

|  方法名  |                 updateUserInfo                 |
| :------: | :--------------------------------------------: |
| 传入参数 | 待更新的用户id，更新后的用户名，密码，角色信息 |
|  返回值  |              用户信息是否更新成功              |

```javascript
POST /users/{userId}
{
    userId: 007,
    username: "qin", 
    password: "111",
    roles: [roleId1, roleId2, ...]
}

Status: 200
```

### 删除用户信息
|  方法名  |    deleteUserInfo    |
| :------: | :------------------: |
| 传入参数 |    待删除的用户Id    |
|  返回值  | 用户信息是否删除成功 |

```javascript
DELETE /users/{userId}

Status: 200
```
## 角色信息接口
### 获取单个角色信息
|  方法名  | getRoleInfoById |
| :------: | :-------------: |
| 传入参数 |   用户角色id    |
|  返回值  |  用户角色信息   |

```javascript
GET /roles/{roleId}

{
    roleId: 001,
    roleName: "管理员",
    roleDescription: "拥有全部权限的管理员",
    rolePowers: [powerId1, powerId2,...]
}
```

### 获取全部角色信息
|  方法名  | getAllRoles  |
| :------: | :----------: |
| 传入参数 |      -       |
|  返回值  | 全部角色信息 |

```javascript
GET /roles

[
    {
        roleId: 001,
    	roleName: "管理员",
    	roleDescription: "拥有全部权限的管理员",
    	rolePowers: [powerId1, powerId2,...]
    },
    ...
]
```

### 添加角色信息
|  方法名  |      addRole      |
| :------: | :----------------------: |
| 传入参数 | 待添加的角色信息 |
|  返回值  |  角色信息是否添加成功  |

```javascript
POST /roles
{
    roleName: "二级审核者",
    roleDescription: "对已审核过的数据再次进行审核",
    rolePowers: [powerId1, powerId2,...]
}

Status 200
```

### 修改角色信息
|  方法名  |      updateRoleInfo      |
| :------: | :----------------------: |
| 传入参数 | 角色id，更新后的角色信息 |
|  返回值  |   角色信息是否修改成功   |

```javascript
POST /roles/{roleId}
{
    roleId: 001,
    roleName: "管理员",
    roleDescription: "拥有全部权限的管理员",
    rolePowers: [powerId1, powerId2,...]
}

Status 200
```
### 删除角色信息
|  方法名  |    deleteRoleInfo    |
| :------: | :------------------: |
| 传入参数 |        角色id        |
|  返回值  | 角色信息是否删除成功 |

```javascript
DELETE /roles/{roleId}

Status 200
```

## 权限信息接口
### 获取单个权限信息
|  方法名  | getPowerInfoById |
| :------: | :--------------: |
| 传入参数 |    用户权限id    |
|  返回值  |   用户权限信息   |

```javascript
GET /powers/{powerId}

{
    powerId: 004,
    powerName: "删除用户",
    powerCode: "user:delete",
}
```

### 获取全部权限信息
|  方法名  |    getAllPowers    |
| :------: | :----------------: |
| 传入参数 |         -          |
|  返回值  | 全部用户的角色信息 |

```javascript
GET /powers

[
    {
        powerId: 001,
        powerName: "查看用户",
        powerCode: "user:view",
    },
    {...},
    ...
]
```
## 展示信息接口
### 病例数展示
|  方法名  |    totalCaseNum    |
| :------: | :----------------: |
| 传入参数 |     当前用户id     |
|  返回值  | 所有病人数量及分布 |

```javascript
GET /cases/caseNum/
{
    total: 100,
    case: [{"name":"女",
    		"value":70},
    		{"name":"男",
    		"value":30}],
}
```
### 结节数展示
|  方法名  |                totalNodeNum                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有用户标记结节数量及分布 |

```javascript
GET /measurements/nodeNum
{
    total: 1583,
    case: [	{value: 321, "name": '歧义候选淋巴结'},
			{value: 158, "name": '结直肠系膜淋巴结'},
			{value: 42, "name": '髂外（髂总）淋巴结'},
			{value: 259, "name": '髂内近端淋巴结'},
			{value: 30, "name": '髂内远端淋巴结'},
			{value: 402, "name": '闭孔头测淋巴结'},
			{value: 117, "name": '闭孔尾测淋巴结'},
			{value: 254, "name": '髂总动脉分叉血管淋巴结'}，]
}
```
### 标注者列表展示
|  方法名  |                getAnnotatorList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者已标注数量,已审核数量,未标注数量 |

```javascript
GET /cases/getAnnotatorList
{
    [{  name:'旋涡鸣人'，
        annotated:30,
        examed: 14,
        unAnnotated:20},
        ......]
}
```
### 病例标注情况列表展示
|  方法名  |                getExamedList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        标注者id        |
|  返回值  | 标注者分配病例及其标注与审核情况 |

```javascript
GET /cases/getExamedList/
{
    annoList: [{    PatientName: 'Li gang',
                    MRN: '0009629786',
                    AccessionNumber: 'CT00566598',
                    IsAnnotated: 'yes',
                    IsExamed: 'yes',
                    StudyDate: '6月20, 2013',
                    AnnotatedNodeNumbers: '68',
                    StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717835',
                    key:'1.2.840.78.75.7.5.1674158.1371717835'
                }, {
                    PatientName: 'Wu Yanzu',
                    MRN: '0009629786',
                    AccessionNumber: 'CT00566598',
                    IsAnnotated: 'yes',
                    IsExamed: null,
                    StudyDate: '6月20, 2013',
                    AnnotatedNodeNumbers: '79',
                    StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717836',
                    key: '1.2.840.78.75.7.5.1674158.1371717836',
                }
    			......]
(IsAnnotated表示该病例是否被标注（'yes'/null），IsExamed表示该病例是否被审核（'yes'/null）)                
}
```
### 标注动态列表展示
|  方法名  |                getAnnotatorActivity                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有标记者的标注动态 |

```javascript
GET /users/getAnnotatorActivity/
{
    annoList: [{name:'旋涡鸣人',
				SericeId: '6354132',
				time: '7/10',},
    			......]
}
```

## 病例管理接口
### 病例列表展示
|  方法名  |                getCaseList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        当前用户id        |
|  返回值  | 当前用户所管理的所有病例数据 |

```javascript
GET /cases/annotatorList/
{

    caseList: [{PatientName: 'Li gang', 
				MRN: '0009629786', 
				AccessionNumber: 'CT00566598', 
				Modality: 'CT', 
				StudyDate: '6月20, 2013', 
				StudyDescription:'Abdomen^HX_ch_abd_c(Adult)',
				StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717835',},
				{…….}
}
(StudyInstanceUID用于跳转ohif相应病例,不可缺少，其余为展示内容，可按情况增减)
```
## 结节搜索接口
### 搜索结果展示
|  方法名  |                getNodeList                |
| :------: | :--------------------------------------------: |
| 传入参数 |        结节搜索条件（分区、直径）       |
|  返回值  | 满足条件的结节列表 |

```javascript
POST /measurements/nodeList
{
    partition:'XM',
    diam: [1.0, 1.5],
    caseList: [ PationtName:'Li gang',
                diam: 1.3,
                partition: 'XM',
                ....],
				{…….}
}
(搜索满足分区'为结直肠系膜淋巴结'(XM),直径在1.0~1.5cm范围内的结节 )
```

------

## 新增API接口(10/12/2020)

------

### 插入case

|  方法名  |      caseInsert      |
| :------: | :------------------: |
| 方法描述 | 向数据库中插入新case |
| 传入参数 |      case(json)      |
|  返回值  |   插入成功返回true   |

```javascript
POST /case/cases/caseInsert
(插入case例子如下：)
{
    "userID": 0,
    "caseID": 10,
    "PatientName": "MISTER^DX",
    "PatientID": "3524578",
    "AccessionNumber": "0000000004",
    "StudyDate": "20010109",
    "modalities": "CT\SR",
    "gender": "male",
    "StudyInstanceUID": "1.2.840.113619.2.67.2158294438.15745010109084247.20000",
    "key": "1.2.840.113619.2.67.2158294438.15745010109084247.20000",
    "annotated": False,
    "examed": False,
}
插入成功返回true,失败返回原因
```

### 修改case的标注者

|  方法名  |              caseModify              |
| :------: | :----------------------------------: |
| 方法描述 | 将某case的标注者改为userID对应标注者 |
| 传入参数 |            caseID, userID            |
|  返回值  |           修改成功返回true           |

```javascript
POST /cases/caseModify

修改成功返回true,失败返回原因
```

### 修改case标注状态

|  方法名  |            caseStatusModify             |
| :------: | :-------------------------------------: |
| 方法描述 | 将某case的标注或审核状态从false变为true |
| 传入参数 |   caseID, userID, "examed/annotated"    |
|  返回值  |            修改成功返回true             |

```javascript
POST /cases/caseStatusModify

修改成功返回true,失败返回原因
```

### 获取标注

|  方法名  |    getMeasurementById    |
| :------: | :----------------------: |
| 传入参数 | StudyInstanceUID，UserID |
|  返回值  | 该用户对该例CT的全部标注 |

```javascript
POST /node_search/users/getMeasurementById

{
   "visible":true,
   "active":false,
   "invalidated":false,
   "handles":
       "start":
           "x":275.42547425474254,
           "y":260.50948509485096,
           "highlight":true,
           "active":false,
       "end":
           "x":293.4634146341463,
           "y":286.87262872628725,
           "highlight":true,
           "active":false,
       "initialRotation":0,
       "textBox":  
           "active":false,    
           "hasMoved":false,    
           "movesIndependently":false, 
           "drawnIndependently":true,
           "allowedOutsideImage":true,
           "hasBoundingBox":true,
           "x":293.4634146341463,
           "y":273.6910569105691,
           "boundingBox":
               "width":10,
               "height":25,
               "left":432.99999999999994,
               "top":437.5,
    "uuid":"44b487fe-e969-4d4c-8a4e-786c3585b124",
    "PatientID":"0009629786",
    "StudyInstanceUID":"1.2.840.78.75.7.5.1674158.1371717835",        "SeriesInstanceUID":"1.3.12.2.1107.5.1.4.73473.30000013061923223125000058318",     "SOPInstanceUID":"1.3.12.2.1107.5.1.4.73473.30000013061923223125000058570",     "frameIndex":0,      "imagePath":"1.2.840.78.75.7.5.1674158.1371717835_1.3.12.2.1107.5.1.4.73473.30000013061923223125000058318_1.3.12.2.1107.5.1.4.73473.30000013061923223125000058570_0",
    "lesionNamingNumber":2,
    "userId":8,
    "toolType":"RectangleRoi",
    "timepointId":"TimepointId",
    "measurementNumber":2,
    "cachedStats":
        "area":240.3515837868401,    
         "count":513,
         "mean":-29.742690058479532,
         "variance":6415.064395882494,
         "stdDev":80.0940971350729,
         "min":-174,
         "max":103,
         "pixels":,
    "viewport":
        "scale":1.44140625,
        "translation":
            "x":0,
            "y":0,
         "voi":
             "windowWidth":315,
             "windowCenter":45,       
          "invert":false,
          "pixelReplication":false,
          "rotation":0,
          "hflip":false,
          "vflip":false,
          "labelmap":false,
          "displayedArea":
              "tlhc":
                  "x":1,
                  "y":1,
               "brhc":
                   "x":512,
                    "y":512
                "rowPixelSpacing":0.7109375,
                "columnPixelSpacing":0.7109375,
                "presentationSizeMode":"NONE",
     "unit":"HU",
}
```



**以下的API需要新建Collection保存启始帧、终止帧**

**{**
    **StudyInstanceUID:"1.2.840.78.75.7.5.1674158.1371717835"**
    **userID: 8**
    **StartingSlice: 5**
    **EndSlice:255**
**}**

### 保存启始帧

|  方法名  |  saveStartingSlicebyId   |
| :------: | :----------------------: |
| 传入参数 | StudyInstanceUID，UserID |
|  返回值  |  启始帧帧数是否插入成功  |

```javascript
POST /startingSliceandEndSlice/saveStartingSlicebyId
{
    StudyInstanceUID:"1.2.840.78.75.7.5.1674158.1371717835",
    userID: 8,
    StartingSlice: 5,
}

Status: 200
```

### 保存终止帧

|  方法名  |     saveEndSlicebyId     |
| :------: | :----------------------: |
| 传入参数 | StudyInstanceUID，UserID |
|  返回值  |  终止帧帧数是否插入成功  |

```javascript
POST /startingSliceandEndSlice/saveEndSlicebyId
{
    StudyInstanceUID:"1.2.840.78.75.7.5.1674158.1371717835",
    userID: 8,
    EndSlice: 5,
}

Status: 200
```

### 获取启始帧、终止帧

|  方法名  |        getStartingandEndSlicebyId        |
| :------: | :--------------------------------------: |
| 传入参数 |         StudyInstanceUID，UserID         |
|  返回值  | 该用户给出的该例CT的启始帧、终止帧的帧数 |

```javascript
POST /startingSliceandEndSlice/getStartingandEndSlicebyId

{
    StartingSlice: 5,
    EndSlice: 255,
}

```

------

## 新增API接口(10/20/2020)

### 获取病人总数

|  方法名  |        getTotalPatientNum        |
| :------: | :------------------------------: |
| 传入参数 |               NULL               |
|  返回值  | case_info数据库中PatientID的总数 |

```javascript
GET /case_info/getTotalPatientNum
{
    totalPatientNum: 20
}

```

### 获取病人性别分布

|  方法名  |  getPatientGenderDistribution   |
| :------: | :-----------------------------: |
| 传入参数 |              NULL               |
|  返回值  | case_info数据库中病人的性别分布 |

```javascript
GET /case_info/getPatientGenderDistribution
{
	gender: [{"name":"女",
        	"value":70},
            {"name":"男",
            "value":30}],
}

```



### 获取病人年龄分布

|  方法名  |    getPatientAgeDistribution    |
| :------: | :-----------------------------: |
| 传入参数 |              NULL               |
|  返回值  | case_info数据库中病人的年龄分布 |

```javascript
GET /case_info/getPatientAgeDistribution
{
	gender: [{"name":"0~14",
        	"value":0},
            {"name":"15~29",
            "value":10},
            {"name":"30~49",
            "value":20},
            {"name":"50~64",
            "value":10},
            {"name":"65以上",
            "value":10}]
}

```



### 获取病例总数

|  方法名  |        getTotalCaseNum        |
| :------: | :---------------------------: |
| 传入参数 |             NULL              |
|  返回值  | case_info数据库中caseID的总数 |

```javascript
GET /case_info/getTotalCaseNum
{
    totalCaseNum: 20
}

```

### 获取结节总数

|  方法名  |        getTotalNodeNum         |
| :------: | :----------------------------: |
| 传入参数 |              NULL              |
|  返回值  | measurements数据库中结节的总数 |

```javascript
GET /measurements/getTotalNodeNum
{
    totalNodeNum: 100
}

```

### 获取结节分区分布

|  方法名  |    getNodePartitionDistribution    |
| :------: | :--------------------------------: |
| 传入参数 |                NULL                |
|  返回值  | measurements数据库中结节的分区分布 |

```javascript
GET /measurements/getPatientAgeDistribution
{
    nodeDistribution: [	{"value": 321, "name": '侧方区'},
						{"value": 158, "name": '非侧方区'}]
}

```

### 获取结节直径分布

|  方法名  |          getNodeDiameterDistribution           |
| :------: | :--------------------------------------------: |
| 传入参数 |                      NULL                      |
|  返回值  | measurements数据库中结节的shortestDiameter分布 |

```javascript
GET /measurements/getNodeDiameterDistribution
{
    node: [	{"value": 321, "name": '0~3'},
			{"value": 158, "name": '3~5'},
          	{"value": 158, "name": '5~10'},
          	{"value": 158, "name": '10以上'}]
}

```

### 获取模型检测进度

|  方法名  |               getModelDetectProcess               |
| :------: | :-----------------------------------------------: |
| 传入参数 |                       NULL                        |
|  返回值  | case_info数据库中结节的status=1的占总case数的比例 |

```javascript
GET /case_info/getModelDetectProcess
{
	percent : [0.5, 10, 20]
}
(百分比，已处理数，总数)
```

## 新增API接口(10/25/2020)

### 获取病例良恶性情况

|  方法名  | getCaseNegativeAndPositive |
| :------: | :------------------------: |
| 传入参数 |            null            |
|  返回值  |    所有病例的良恶性数值    |

```javascript
GET /case_info/getCaseNegativeAndPositive
{
    "positive":120,
    "negative":250
}
(良性个数，恶性个数)
```

### 获取每日新增病例数

|  方法名  |    getDailyAddCase     |
| :------: | :--------------------: |
| 传入参数 |          null          |
|  返回值  | 近20天内的每日新增病例 |

```javascript
GET /case_info/getDailyAddCase
{
	"date":["2020/10/12","2020/10/13","2020/10/14"]
    "DailyAdd":[150,140,124]
}
(日期，每日新增 ps:个数一致，分别对应,如：date[0]新增了DailyAdd[0]个病例)
```

### 获取所有病人病例情况

|  方法名  |   getCaseList    |
| :------: | :--------------: |
| 传入参数 |       null       |
|  返回值  | 所有病人病例情况 |

```javascript
GET /case_info/getCaseList
{
      "caseList":[
          {
            "userID": 0,
            "key":"0009369854",
            "PatientName": "ji lu xiu",
            "PatientID": "0009369854",
            "patientSex": "男",
            "case":[
                {
                    "key":"20040310",
                    "StudyDate":"20040310",
                    "caseNum":2,
                    "caseItem":[
                        {
                            "key":"1.2.840.78.75.7.5.280728.1370251044",
                            "AccessionNumber":"CT00549838",
                            "StudyInstanceUID":"1.2.840.78.75.7.5.280728.1370251044",
                            "modalities":"CT\\SR" 
                        },
                        {
                            "key":"1.3.840.78.75.7.5.280728.7841241044",
                            "AccessionNumber":"CT00549838",
                            "StudyInstanceUID":"1.3.840.78.75.7.5.280728.7841241044",
                            "modalities":"CT\\SR" 
                        },					                
                    ]
                },
                {
                    "key":"20140601",
                    "StudyDate":"20140601",
                    "caseNum":1,
                    "caseItem":[
                        {
                            "key":"1.2.840.78.75.7.5.280728.1370251044",
                            "AccessionNumber":"CT00549838",
                            "StudyInstanceUID":"1.2.840.78.75.7.5.280728.1370251044",
                            "modalities":"CT\\SR" 
                        }				                
                    ]
                  }   
              ]
          },
          {
            "userID": 0,
            "key":"0009629786",
            "PatientName": "li gang",
            "PatientID": "0009629786",
            "patientSex": "女",
            "case":[
                {
                    "key":"20130620",
                    "StudyDate":"20130620",
                    "caseNum":1,
                    "caseItem":[
                        {
                            "key":"1.2.840.78.75.7.5.280728.1370251041",
                            "AccessionNumber":"CT00549838",
                            "StudyInstanceUID":"1.2.840.78.75.7.5.280728.1370251044",
                            "modalities":"CT\\SR" 
                        }					                
                    ]
                },
                {
                    "key":"20140601",
                    "StudyDate":"20140601",
                    "caseNum":1,
                    "caseItem":[
                        {
                            "key":"1.2.840.78.75.7.5.280728.1370251044",
                            "AccessionNumber":"CT00549838",
                            "StudyInstanceUID":"1.2.840.78.75.7.5.280728.1370251044",
                            "modalities":"CT\\SR" 
                        }				                
                    ]
                }   
              ]       
          }
      ]
}
(结构逻辑就是：caseList=
 [
    {	病人:,
     	病例:[
     			{
     				检查日期:
     				具体当日病例:{}
    			}
     		]
    },
    {
       病人:,
       病例:[
           		{
                    检查日期:
                    具体当日病例:{}
                }
       		]
    }
]，病人的key值是他的id值，检查日期里的key值是日期，具体病例的key值是病例uid，在检查日期里的caseNum是当日检查的次数，也是当日检查的病例数)
```

### measurement更新

|  方法名  |      measurementsUpdate       |
| :------: | :---------------------------: |
| 传入参数 |       measurements列表        |
|  返回值  | 更新成功返回200，失败返回原因 |

```javascript
POST /measurements/measurementsUpdate
传入{
	[标注数据列表]
}
更新成功返回200，失败返回原因
```

## 新增api需求（10/27/2020）

###  获取每日新增病例数

|  方法名  |      getDailyAddCase       |
| :------: | :------------------------: |
| 传入参数 |   （beginDate, endDate）   |
|  返回值  | 两date之间的每日检查病例数 |

```javascript
GET /case_info/getDailyAddCase
{
	"date":["2020/10/12","2020/10/13","2020/10/14"]
    "DailyAdd":[150,140,124]
}
(日期，每日新增 ps:个数一致，分别对应,如：date[0]新增了DailyAdd[0]个病例)
```

### 获取所有病人病例情况

|  方法名  |   getCaseList    |
| :------: | :--------------: |
| 传入参数 |       null       |
|  返回值  | 所有病人病例情况 |

```javascript
GET 
[{
      "PatientName": "ji lu xiu",
      "PatientID": "0009369854",
      "PatientSex": "女",
      "PatientAge":"36",
      "dateList":[	//该病人在XX日子进行了检查
          {
              "StudyDate":"20130603",
              "caseNum":1,
              "caseList":[	//该病例在某天进行了几次检查
                  {
                      "caseID":"0009369854:1.2.840.78.75.7.5.280728.1370251044:20130603",
                      "AccessionNumber":"CT00549838",
                      "StudyInstanceUID": "1.2.840.78.75.7.5.280728.1370251044",
                      "modelStatus":false, 
                      "annotatedStatus":false,
                  }, {
                      ...
                  },.....                         
              ]
          },  {
              ......
          }, {
              ......
          }.....
        ]
    },{
       .....
    }
]
[
        {
      "PatientName": "ji lu xiu",
      "PatientID": "0009369854",
      "PatientSex": "女",
      "PatientAge":"36",
      "dateList":[
          {
              "StudyDate":"20130603",
              "caseNum":2,
              "caseList":[
                  {
                      "caseID":"0009369854:1.2.840.78.75.7.5.280728.1370251044:20130603",
                      "AccessionNumber":"CT00549838",
                      "StudyInstanceUID": "1.2.840.78.75.7.5.280728.1370251044",
                      "modelStatus":false, 
                      "annotatedStatus":false,
                  },
                  {
                    "caseID":"0009369854:1.2.840.78.75.7.5.280728.1467894597:20130603",
                    "AccessionNumber":"CT00549838",
                    "StudyInstanceUID": "1.2.840.78.75.7.5.280728.1467894597",
                    "modelStatus":false, 
                    "annotatedStatus":false,
                },                              
              ]
          },  
        ]
    },
    {
      "PatientName": "tao qi fa",
      "PatientID": "0008987865",
      "PatientSex": "男",
      "PatientAge":"65",
      "dateList":[
          {
              "StudyDate":"20040310",
              "caseNum":1,
              "caseList":[
                  {
                      "caseID":"0008987865:1.2.840.78.75.7.5.1842989.1364010904:0008987865",
                      "AccessionNumber":"CT00549838",
                      "StudyInstanceUID":"1.2.840.78.75.7.5.1842989.1364010904",
                      "modelStatus":false, 
                      "annotatedStatus":true,
                  },                                    
              ]
          },
          {
            "StudyDate":"20040310",
            "caseNum":2,
            "caseList":[
                {
                    "caseID":"0008987865:1.2.840.78.75.7.5.1842989.1364010904:0008987865",
                    "AccessionNumber":"CT00549838",
                    "StudyInstanceUID":"1.2.840.78.75.7.5.1842989.1364010904",
              
]
```

### 修改标注状态（无需标注->待标注）

|  方法名  |        modifyAnnotatedStatus        |
| :------: | :---------------------------------: |
| 传入参数 | {"caseID":["caseID1","caseID2"...]} |
|  返回值  |                                     |

```javascript
POST /case_info/modifyAnnotatedStatus
{}
status:200
```

### 审核者获取对应标注者列表

|  方法名  | getAnnotatorListByReviewer |
| :------: | :------------------------: |
| 传入参数 |        审核者userID        |
|  返回值  |      标注者userID列表      |

```javascript
POST /annotator_reviewer/getAnnotatorListByReviewer
[{
    'userID': 0,
    'userName': admin,
}{
    ...
}]
```

### 给审核者分配标注者

|  方法名  | assignReviewer |
| :------: | :------------: |
| 传入参数 |      如下      |
|  返回值  |    分配结果    |

```javascript
POST /annotator_reviewer/assignReviewer
传入参数：{
    'reviewerID': 0,
    'annotatorID': [1, 2, 3]
}
status: 200
```

### 修改模型检测状态码（未检测->已检测）

|  方法名  | modifyModelStatus |
| :------: | :---------------: |
| 传入参数 |      caseID       |
|  返回值  |     修改结果      |

```javascript
POST /case_info/modifyModelStatus
{}
status:200
```

## 新增api需求（10/29/2020）

###  获取已有分配关系

|  方法名  |       getAssignedRelations        |
| :------: | :-------------------------------: |
| 传入参数 |               null                |
|  返回值  | 全部annotator、reviewer的对应关系 |

```javascript
GET /annotator_reviewer/getAssignedRelations
{
    "reviewer":[
        {
            "userID":2,
            "name":"huanghao",
            "annotators":[6,5,4,14]//这个审核者所管理的标注者的userID
        },
        {
            "userID":3,
            "name":"yangxu",
            "annotators":[25,24,23,5]
        }，
        ...
    ],
    "annotator":[
        {
            "name":"panzhen",
            "userID":6,
            "reviewers":["huanghao","huanghao1"]
            //这个标注者所属的审核者的name，这里要userID是因为标注者并不会改动他的审核者
        },
        {
            "name":"qin",
            "userID":5,
            "reviewers":["huanghao","yangxu"]
        }，
        ...
     ]
}
```

## 新增api需求（10/30/2020）

###  获取标注者列表

|  方法名  | getAnnotatorListAndCase |
| :------: | :---------------------: |
| 传入参数 |          null           |
|  返回值  | 标注者列表及其分配情况  |

```javascript
GET /user_case/getAnnotatorListAndCase
[{
    "userID": 2,
    "userName": "huanghao",
    "assignedCaseNum": 1, 	//已经分配给该标注者的case数量
    "assignedCaseList": [3]	//已经分配给该标注者的caseID列表，未分配时为[]
  }, {
    "userID": 3,
    "userName": "yangxu",
    "assignedCaseNum": 2, 
    "assignedCaseList": [1, 2]
  }]
```

###  修改标注者case分配情况

|  方法名  | modifyAnnotatorCase  |
| :------: | :------------------: |
| 传入参数 | userID, caseID的list |
|  返回值  |       修改结果       |

```javascript
GET /user_case/modifyAnnotatorCase
[{
    "userID":2,
    "assignedCaseList":[1, 2, 3] //分配给该标注者的caseID列表。
}]
```

## 新增api需求（10/31/2020-from csh）

### 标注者标注管理界面获取case信息及相应的状态信息

|  方法名  |                    getAnnotatorsCaseInfo                     |
| :------: | :----------------------------------------------------------: |
| 传入参数 |                            userID                            |
|  返回值  |        该标注者所需标注的所有case信息及相应case的状态        |
|   备注   | 如果statusOfAnnotated、statusOfReviewed字段相应信息无法和其他字段同时获取，可以分开写，但希望最后能按下方给出的格式组织数据返回。如果文档中关于statusOfAnnotated、statusOfReviewed两个字段的描述有问题联系csh一起讨论 |

```javascript
POST /case_info/getAnnotatorsCaseInfo
{
    userID: 6
}

[
  {
    PatientName: 'ji lu xiu',
    PatientID: '009369854',
    AccessionNumber: 'CT00549838',
    StudyDate: '20130603',
    statusOfAnnotated: ['0'], //该标注者对该例case的标注状态，'0'表示未标注，’1’表示已标注
    statusOfReviewed: ['0'], //该标注者的审核者对该例case的审核状态，'0'表示未审核，’1’表示已审核
    StudyInstanceUID: '1.2.840.78.75.7.5.280728.1370251044'
  },
  {
    PatientName: 'li gang',
    PatientID: '0009629786',
    AccessionNumber: 'CT00566598',
    StudyDate: '20130620',
    statusOfAnnotated: ['1'],
    statusOfReviewed: ['0'],
    StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717835'
  },
  {
    PatientName: 'yang cong ying',
    PatientID: '0001053245',
    AccessionNumber: 'CT00705850',
    StudyDate: '20131030',
    statusOfAnnotated: ['0'],
    statusOfReviewed: ['0'],
    StudyInstanceUID: '1.2.840.78.75.7.5.10839406.1383139266'
  },
  {
    PatientName: 'tao qi fa',
    PatientID: '0008987865',
    AccessionNumber: 'CT00471087',
    StudyDate: '20130323',
    statusOfAnnotated: ['1'],
    statusOfReviewed: ['1'],
    StudyInstanceUID: '1.2.840.78.75.7.5.1842989.1364010904'
  }
]
```

![Snipaste_2020-10-31_20-26-42](..\image\Snipaste_2020-10-31_20-26-42.png)

相应的前端UI

### 审核者审核标注管理界面获取case信息及相应的状态信息

|  方法名  |                     getReviewersCaseInfo                     |
| :------: | :----------------------------------------------------------: |
| 传入参数 |                            userID                            |
|  返回值  | 该审核者所需审核的所有case信息、标注相应case的标注人员及相应case的状态 |
|   备注   | 如果AnnotatorList、statusOfAnnotated、statusOfReviewed字段相应信息无法和其他字段同时获取，可以分开写，但希望最后能按下方给出的格式组织数据返回。如果文档中关于statusOfAnnotated、statusOfReviewed两个字段的描述有问题联系csh一起讨论 |

```javascript
POST /case_info/getReviewersCaseInfo
{
    userID: 2
}


[
  {
    PatientName: 'ji lu xiu',
    PatientID: '009369854',
    AccessionNumber: 'CT00549838',
    StudyDate: '20130603',
    AnnotatorList: ['huanghao','pz'],//该例case的标注人员列表
    statusOfAnnotated: ['0','0'],//该例case每个标注人员完成标注工作的标注状态，'0'表示未标注，’1’表示已标注
    statusOfReviewed: ['-1'],
    StudyInstanceUID: '1.2.840.78.75.7.5.280728.1370251044'
  },
  {
    PatientName: 'li gang',
    PatientID: '0009629786',
    AccessionNumber: 'CT00566598',
    StudyDate: '20130620',
    AnnotatorList: ['huanghao','pz'],
    statusOfAnnotated: ['1','0'],
    statusOfReviewed: ['0'],
    StudyInstanceUID: '1.2.840.78.75.7.5.1674158.1371717835'
  },
  {
    PatientName: 'yang cong ying',
    PatientID: '0001053245',
    AccessionNumber: 'CT00705850',
    StudyDate: '20131030',
    AnnotatorList: ['huanghao','pz'],
    statusOfAnnotated: ['0','1'],
    statusOfReviewed: ['0'],
    StudyInstanceUID: '1.2.840.78.75.7.5.10839406.1383139266'
  },
  {
    PatientName: 'tao qi fa',
    PatientID: '0008987865',
    AccessionNumber: 'CT00471087',
    StudyDate: '20130323',
    AnnotatorList: ['huanghao','pz'],
    statusOfAnnotated: ['1','1'],
    statusOfReviewed: ['1'],
    StudyInstanceUID: '1.2.840.78.75.7.5.1842989.1364010904'
  }
]
```

![Snipaste_2020-10-31_20-26-07](..\image\Snipaste_2020-10-31_20-26-07.png)

### 标注者所需标注case的标注工作、审核工作情况统计

|  方法名  |                   getAnnotatorsCasesStatus                   |
| :------: | :----------------------------------------------------------: |
| 传入参数 |                            userID                            |
|  返回值  | 该标注者所需标注的case中，已标注的case数，未标注的case数，已审核的case数，未审核的case数 |

```javascript
POST /case_info/getAnnotatorsCasesStatus
{
    userID: 6
}

[
    {
        annotatedCase:2,
        unannotatedCase:2,
        reviewedCase:1,
        unreviewedCase:3,
    }
]
```

### 审核者所需审核case的标注工作、审核工作情况统计

|  方法名  |                   getReviewersCasesStatus                    |
| :------: | :----------------------------------------------------------: |
| 传入参数 |                            userID                            |
|  返回值  | 该审核者所需审核的case中，已标注的case数，未标注的case数(这里关于标注状态的统计针对的是case，如果是合并审核的逻辑，比如标注者A和B都负责标注case1, A的annotated为true，B的annotated为true，那么这一例case的标注状态为已标注)，已审核的case数，未审核的case数 |

```javascript
POST /case_info/getReviewersCasesStatus
{
    userID: 2
}

[
    {
        annotatedCase:2, // 
        unannotatedCase:2,
        reviewedCase:1,
        unreviewedCase:3,
    }
]
```

------

## 新增api需求(11/2/2020)

### 返回所有待标注的病例数据

|  方法名  |                   getAnnotateList                   |
| :------: | :-------------------------------------------------: |
| 传入参数 |                        null                         |
|  返回值  | 所有待标注的病例列表（annotatedStatus不为-1的时候） |

```javascript
GET /case_info/getAnnotateList
[  {
    PatientName: 'yang cong ying',
    PatientID: '0001053245',
    assignedAnnotator: ['huanghao','pz'],
    caseID: '0001053245:1.2.840.78.75.7.5.10839406.1383139266:1.3.12.2.1107.5.1.4.66043.30000013103006375212500083837'
  },{
    PatientName: 'tao qi fa',
    PatientID: '0008987865',
    assignedAnnotator: [],
    caseID: '0008987865:1.2.840.78.75.7.5.1842989.1364010904:1.3.12.2.1107.5.1.4.73473.30000013032215343534300021955'
  }]
```

## 
