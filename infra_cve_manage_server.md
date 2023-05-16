## Infra CVE Manage Server

### 背景
Infra团队维护的项目日益增多，需要一个服务发现各个项目涉及的CVE漏洞，通知相关的责任人并跟踪CVE漏洞的处理情况。

### 服务架构
在产品架构设计中，为了满足不同领域的特定需求，往往使用多视图描述架构，接下来通过4+1视图来描述本服务的架构。

- 用例视图

<img src='https://raw.githubusercontent.com/nicliuqi/docs/main/%E7%94%A8%E4%BE%8B%E8%A7%86%E5%9B%BE.png' width=600 height=350 alt='用例视图'/>

在本服务中，项目的维护者在登陆（因维护者都提供了邮箱，可通过邮箱验证的方式登陆）后可查询负责的项目、负责项目涉及的包、负责项目涉及的CVE漏洞以及修复CVE。

- 逻辑视图

<img src='https://raw.githubusercontent.com/nicliuqi/docs/main/%E9%80%BB%E8%BE%91%E8%A7%86%E5%9B%BE.png' width=600 height=350 alt='用例视图'/>

逻辑视图根据用例视图设计。
Project表字段包含了一个项目的地址、分支、维护者以及维护者邮箱；
Pakcge表字段包含了一个包的名称、版本以及所属的项目id；
Vulnerability表字段包含了一个漏洞的编号、状态、修复者、创建时间、更新时间、所属包

- 流程视图

<img src='https://raw.githubusercontent.com/nicliuqi/docs/main/%E6%B5%81%E7%A8%8B%E8%A7%86%E5%9B%BE.png' width=600 height=350 alt='流程视图'/>
