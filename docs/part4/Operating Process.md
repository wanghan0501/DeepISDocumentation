| 标注系统                                                     | 展示系统                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 病例及人员分配工作由管理者admin完成，admin依照实际情况新建审核者、标注者角色；<br/>admin将标注者分配给审核者进行审核（annotator_reviewer表：userID<审核者>,userID<标注者>）；<br/>admin将病例分配给标注者（user_case表：userID<标注者>，caseID）；<br/>标注者对case_info表中annotatedStatus为0的数据开始标注。 | 面向医院，使用者为hospital（即设置为特殊的userID），可以自动连接至医院PACS系统（也可手动上传dicom文件，后台模拟插入PACS操作），<br/>模型进行检测后，将相关病例数据插入至case_info表（增加modelStatus字段表示本例数据的模型处理进度：False-待检测；<br/>True-已检测；增加annotateStatus字段），检测出的结节数据插入至measurements表(以userID作为标识，区分系统检出结节与医生标注结节)；<br/>hospital手动选择需要标注的case_info表中数据（annotatedStatus字段默认值为-1，被选中需要标注后置为0，分配给一人标注置为1，分配给两人标注置为2，以此类推）。 |

------



| case_info                                                    | measurement                                                  | user_case                                                    | annotator_reviewer                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| "PatientName": <br/>"PatientID":<br/>"StudyInstanceUID":<br/>"SeriesInstanceUID": <br/>"AccessionNumber":<br/> "PatientBirthDate": <br/>"StudyDate": <br/>"PatientAge":<br/>"PatientSex":<br/>“caseID”:<br/>“modelStatus”:<br/>“annotatedStatus”:<br/>“provedStatus”:<br/> | "userID" : 表示该条信息的所属者，<br/>"annotator" : 表示该条信息的标注者,<br/>"uuid" : "1e762d5e-f7a7-4c4d-95aa-3923112f5a56",<br/>"PatientID" : "0009629786",<br/>"StudyInstanceUID" : "1.2.840.78.75.7.5.1674158.1371717835",<br/>"SeriesInstanceUID" : "1.3.12.2.1107.5.1.4.73473.30000013061923223125000058318",<br/>“SOPInstanceUID” : “1.3.12.2.1107.5.1.4.73473.30000013061923223125000058571”,等信息 | “userID":<br/>“caseID":<br/>“annotated”:<br/><br/>----------------<br/>标注者+病例<br/>对应关系<br/>及<br/>标注情况、审核情况 | “reviewerID":<br/>“annotatorID":<br/><br/>----------<br/>审核者+标注者<br/>对应关系 |

- "caseID" = "PatientID" + ":" + "StudyInstanceUID" + ":" + "SeriesInstanceUID"

- modelStatus:初始值为False，表示未经模型检测；模型完成对本病例检测后，置值为True

- annotatedStatus:初始值为-1，表示无需进行标注；置值为0，表示待标注；置值为1，表示分配给了一个标注者；置值为2，表示分配给两个标注者；以此类推

- PatientAge = int(StudyDate 年份数值) – int(PatientBirthDate 年份数值)

- provedStatus:初始值为-1，表示未进行审核；置值为0，表示正在审核标注；置值为1，表示已经审核完

  ------

  

| **ai_measurements**                                          |      | **hospital_user_case**                                       |
| ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| "userID" : 该模型的userID，<br/>"annotator" : 该模型的userID,<br/>"uuid" : "1e762d5e-f7a7-4c4d-95aa-3923112f5a56",<br/>"PatientID" : "0009629786",<br/>"StudyInstanceUID" : "1.2.840.78.75.7.5.1674158.1371717835",<br/>"SeriesInstanceUID" : "1.3.12.2.1107.5.1.4.73473.30000013061923223125000058318",<br/>“SOPInstanceUID” : “1.3.12.2.1107.5.1.4.73473.30000013061923223125000058571”,等信息 |      | “userID": 医院使用者的userID<br/>“caseID":<br/>---------------------<br/>医院使用者+病例对应关系<br/>存在这条记录表示该医院使用者对该病例的模型检测结果进行了修改 |

- ai_measurements记录模型检测结果，其中，不同版本的模型有自己单独的userID

------



| measurements                                                 |                                | reviewer_measurements                                        |                    | fresher_measurements |
| ------------------------------------------------------------ | ------------------------------ | ------------------------------------------------------------ | ------------------ | -------------------- |
| "longestDiameter" : "21.1",<br/>"shortestDiameter" : "10.5",<br/>"uuid" : "1e762d5e-f7a7-4c4d-95aa-3923112f5a56",<br/>"PatientID" : "0009629786",<br/>"StudyInstanceUID" : "1.2.840.78.75.7.5.1674158.1371717835",<br/>"SeriesInstanceUID" : "1.3.12.2.1107.5.1.4.73473.30000013061923223125000058318",<br/>“SOPInstanceUID” : “1.3.12.2.1107.5.1.4.73473.30000013061923223125000058571”,<br/>“annotator”:userID,等信息 | ----><br/>逻辑处理<br/>NMS合并 | "longestDiameter" : "21.1",<br/>"shortestDiameter" : "10.5",<br/>"uuid" : "1e762d5e-f7a7-4c4d-95aa-3923112f5a56",<br/>"PatientID" : "0009629786",<br/>"StudyInstanceUID" : "1.2.840.78.75.7.5.1674158.1371717835",<br/>"SeriesInstanceUID" : "1.3.12.2.1107.5.1.4.73473.30000013061923223125000058318",<br/>“SOPInstanceUID” : “1.3.12.2.1107.5.1.4.73473.30000013061923223125000058571”,<br/>“annotator”:userIDs,等信息 | <-----<br/>NMS合并 |                      |

- reviewer_measurements 2个api：暂存，只修改表中数据；提交，修改表中数据并修改case_info表中provedStatus状态码

------



| user_info                                                    | role_info                                                    | power_info                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| “userID”: 主键，int型，从0开始编码<br/>“username”:用户名<br/>“password”:用户密码<br/>“roles”:用户的角色信息，对应roleID（只能有一个角色：管理员、标注者、审核者或使用者） | “roleID":主键，int型，从0开始编码<br/>“roleName”:角色名<br/>“roleDescription”:角色描述<br/>“powers”:权限信息，对应powerID，可以是多个权限组成的list，也可以是单个权限 | “powerID”:权限ID，主键，int型，从0开始编码<br/>“powerName”:权限名称<br/>“powerDescription”:权限描述<br/>“powercode”：权限编码 |

- 用户权限管理

