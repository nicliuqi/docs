## QuickIssue

### 服务介绍
- 简介
QuickIssue，是一个基于代码托管平台提供的接口刷新数据，为openEuler社区开发者提供issue和Pull Request看板以及快速提交issue功能的服务。
- 应用场景
  - 快速提交issue
    用户可通过QuickIssue的landscape快速定位到需要提交issue的SIG和仓库。有对应代码托管平台账号的用户会被引导至代码托管平台的issue提交页面自行编辑提交；无账号的用户可通过邮箱验证的方式提交issue，成功提交后服务会记录提交者的邮箱，便于后续issue跟踪。
  - issue跟踪
    服务会跟踪通过邮箱验证方式提交的issue。当有其他用户（非机器人）在issue下评论时，服务会发送附带评论内容的邮件通知issue提交者；当issue的状态发生变更时，服务会发送状态变更邮件通知issue提交者。
  - 看板查询
    想要快速高效地搜索到自己关心的看板数据？issue看板和Pull Request看板提供了丰富的查询功能。
    看板最上方的搜索框支持多个字段（仓库、标题等）的模糊匹配。看板中带有漏斗标志的字段都支持进一步筛选。值得注意的是，issue和PR可选择查看多个状态；而标签既可选择一条issue或PR中同时存在的标签，也可排除掉需过滤的标签。
    issue和Pull Request看板同时还提供了两个时间维度的排序，用户可选择按创建时间或更新时间的顺序或逆序排序。
  - 数据导出（暂未开放）

### 最新动态

2022年11月
  | 序号 | 动态名称 | 动态描述 
  |  :---:  |  :---: | :---: 
   1 | 模糊匹配优化 | 优化了issue看板和Pull Request看板多个搜索框的模糊匹配机制，忽略大小写
   2 | 标签过滤 | Pull Request看板新增标签过滤功能
   3 | 查询优化 | 优化SQL查询，提高接口的访问速度
   4 | issue状态变更提醒 | 为通过邮箱提交issue的用户提供issue状态变更的邮件通知

2022年10月
  | 序号 | 动态名称 | 动态描述
  |  :---:  |  :---: | :---: 
   1 | QuickIssue服务上线 |  为openEuler社区开发者提供代码托管平台的issue看板以及快速提交issue服务
   2 | issue评论提醒 | 为通过邮箱提交issue的用户提供issue评论的邮件通知
   3 | Pull Request看板上线 | 为openEuler社区开发者提供代码托管平台的Pull Request看板

### API参考
- API概览
  - 提交issue
    | API | 说明 
    |  :---:  |  :---:
    | 邮箱验证 | 用户在快速提交issue时通过邮箱接收验证码
    | 上传图片 | 将图片上传至代码托管平台的服务器，返回图片链接
    | 提交issue | 向代码托管平台的某个仓库提交issue
    | 上传附件 | 将附件上传至代码托管平台的服务器，并绑定已创建的issue
    
  - issue看板
    | API | 说明
    | :---: | :---:
    | issue列表 | 所有openeuler/src-openeuler组织下仓库的issue列表
    | issue指派者列表 | 所有issue指派者的列表
    | issue提交人列表 | 所有issue提交人的列表
    | issue分支列表 | 所有issue指定分支的列表
    | issue标签列表 | 所有issue标签的列表
    | issue类型列表 | 所有issue类型的列表
    | 仓库列表 | 所有openeuler/src-openeuler组织下仓库的列表
    
  - Pull Request看板
    | API | 说明
    | :---: | :---
    | Pull Request列表 | 所有openeuler/src-openeuler组织下仓库的Pull Request列表
    | Pull Request指派者列表 | 所有Pull Request指派者的列表
    | Pull Request提交人列表 | 所有Pull Request提交人的列表
    | Pull Request分支列表 | 所有Pull Request指定分支的列表
    | Pull Request标签列表 | 所有Pull Request标签的列表
    | Pull Request仓库列表 | 所有openeuler/src-openeuler组织下仓库的Pull Request所属仓库的列表
    | SIG列表 | 所有Pull Request所属的SIG列表
    
  - 标签
    | API | 说明
    | :---: | :---
    | 标签列表 | 企业所有标签的列表
    
- API
**endpoint**: https://ipb.osinfra.cn

  - 邮箱验证
    - 功能介绍
      用户在快速提交issue时通过邮箱接收验证码
    - URI
      POST /verify
    - 请求参数
      | 参数 | 是否必选 | 参数类型 | 描述
      | :---: | :---: | :---: | :---
      | email | 是 | string | 待接收验证码的邮箱地址
      
  - 上传图片
    - 功能介绍
      将图片上传至代码托管平台的服务器，返回图片链接
    - URI
      POST /image
    - 请求参数
      | 参数 | 是否必选 | 参数类型 | 描述
      | :---: | :---: | :---: | :---
      | file | 是 | file | 待上传的图片

  - 提交issue
    - 功能介绍
      向一个仓库提交issue
    - URI
      POST /issues
    - 请求参数
      | 参数 | 是否必选 | 参数类型 | 描述
      | :---: | :---: | :---: | :---
      | email | 是 | string | 已接收验证码的邮箱地址
      | code | 是 | string | 已接收的验证码
      | project_id | 是 | int | 待提交issue所属仓库的企业id
      | issue_type_id | 是 | int | 待提交issue类型的企业id
      | title | 是 | string | 待提交issue的标题
      | description | 是 | string | 待提交issue的内容
      | file | 否 | file | 待上传的附件
      
  - 上传附件
    - 功能介绍
      上传附件并绑定issue
    - URI
      POST /attachment
    - 请求参数
      | 参数 | 是否必选 | 参数类型 | 描述
      | :---: | :---: | :---: | :---
      | file | 是 | file | 待上传的附件
      | attach_id | 是 | string | 待绑定issue的企业id
      
  - issue列表
    - 功能介绍
      获取issue列表
    - URI
      GET /issues
    - 请求参数
      | 参数 | 是否必选 | 参数类型 | 描述
      | :---: | :---: | :---: | :---
      | org | 否 | string | issue所属组织
      | repo | 否 | string | issue所属仓库
      | sig | 否 | string | issue所属SIG
      | state | 否 | string | issue的状态
      | number | 否 | string | issue编号
      | author | 否 | string | 提交人
      | assignee | 否 | string | 指派者
      | branch | 否 | string | 指定分支
      | label | 否 | string | issue的标签
      | exclusion | 否 | string | 过滤的issue标签
      | issue_state | 否 | string | issue的具体状态
      | issue_type | 否 | string | issue的类型
      | priority | 否 | int | 优先级
      | sort | 否 | string | 排序方式，默认created_at
      | direction | 否 | string | 排序的顺序，默认desc
      | search | 否 | string | 模糊搜索字段，匹配issue编号、仓库和标题
      | page | 否 | int | 页数，默认1
      | per_page | 否 | int | 每页数量，默认10，最大100
      
  - issue指派者列表
    - 功能介绍
      获取issue所有指派者的列表
    - URI
      GET /issues/assignees
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配issue的指派者
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - issue提交人列表
    - 功能介绍
      获取issue所有提交人的列表
    - URI
      GET /issues/authors
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配issue的提交人，keyword中包含"@"时匹配reporter
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - issue分支列表
    - 功能介绍
      获取issue所有指定分支的列表
    - URI
      GET /issues/branches
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配issue的指定分支
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - issue标签列表
    - 功能介绍
      获取issue所有标签的列表
    - URI
      GET /issues/labels
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配issue的标签
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - issue类型列表
    - 功能介绍
      获取issue所有类型的列表
    - URI
      GET /issues/types
    - 请求参数
      无
       
  - 仓库列表
    - 功能介绍
      获取所有openeuler/src-openeuler组织下仓库的列表
    - URI
      GET /repos
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配issue的指派者
       | sig | 否 | string | 仓库所属SIG
       | direction | 否 | string | 排序，默认按仓库名称排序
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - Pull Request列表
    - 功能介绍
      获取所有openeuler/src-openeuler组织下仓库的Pull Request列表
    - URI
      GET /pulls
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | org | 否 | string | Pull Request所属组织
       | repo | 否 | string | Pull Request所属仓库
       | sig | 否 | string | Pull Request所属SIG
       | state | 否 | string | Pull Request的状态
       | ref | 否 | string | Pull Request指定的分支
       | author | 否 | string | 提交人
       | assignee | 否 | string | 指派者
       | sort | 否 | string | 排序方式，默认created_at
       | direction | 否 | string | 排序的顺序，默认desc
       | label | 否 | string | Pull Request的标签
       | exclusion | 否 | string | 过滤的Pull Request标签
       | search | 否 | string | 模糊搜索字段，匹配SIG、仓库和标题
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - Pull Request指派者列表
    - 功能介绍
      获取所有Pull Request指派者的列表
    - URI
      /pulls/assignees
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配Pull Request的指派者
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - Pull Request提交人列表
    - 功能介绍
      - 获取所有Pull Request提交人的列表
    - URI
      GET /pulls/authors
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配Pull Request的提交人
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - Pull Request分支列表
    - 功能介绍
      获取所有Pull Request的分支列表
    - URI
      GET /pulls/refs
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配Pull Request的指定分支
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - Pull Request标签列表
    - 功能介绍
      获取所有Pull Request的标签列表
    - URI
      GET /pulls/labels
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配Pull Request的标签
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - Pull Request仓库列表
    - 功能介绍
      获取所有Pull Request的仓库列表
    - URI
      GET /pulls/repos
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配Pull Request的所属仓库
       | page | 否 | int | 页数，默认1
       | per_page | 否 | int | 每页数量，默认10，最大100
       
  - SIG列表
    - 功能介绍
      获取所有SIG的列表
    - URI
      GET /pulls/sigs
    - 请求参数
       | 参数 | 是否必选 | 参数类型 | 描述
       | :---: | :---: | :---: | :---
       | keyword | 否 | string | 模糊匹配Pull Request的所属SIG
       
### 常见问题
Q: 在进入提交issue界面后，弹框显示 `AxiosError: Network Error`，应该如何解决？
A: 当进入提交issue界面后，服务会与代码托管平台进行数据交互，获取实时的issue类型（issue_type_id在前端重定向时会用到）。发生上述错误多是因为未获取到issue类型，建议等待一段时间后再重试。

### 联系
有任何关于QuickIssue的意见或建议，请发邮件至[infra@openeuler.org](https://mailweb.openeuler.org/postorius/lists/infra.openeuler.org/)。
