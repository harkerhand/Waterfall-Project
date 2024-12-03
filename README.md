# Waterfall-Project

## 简介  
本项目为**软件工程导论大作业**，实现了一个以**瀑布模型**为核心内容的网页应用。用户通过该网页可以：  
- **学习知识点**：展示瀑布模型的相关知识点及其关系（以知识图谱形式呈现）。  
- **参与测试**：随机抽取数据库中的题目进行作答，系统根据答案判定对错，并返回分数和正确答案。  

该项目以知识传播与学习反馈为目的，为用户提供了学习与自测一体化的功能。  

---

## 项目结构 
本项目采用**前后端分离**的架构设计，主要分为以下三个部分：  

### 1. 前端（Frontend）  
- **代码存放路径**：`frontend/` 文件夹  
- **开发技术**：使用 **Vue.js** 框架构建用户界面。  
- **功能模块**：
  - 知识点的可视化展示。
  - 用户答题界面与提交交互。
  - 测试结果的动态反馈与显示。

### 2. 接口（API）  
- **代码存放路径**：`api/` 文件夹  
- **开发技术**：使用 **Java** 和 **Spring Boot** 框架构建后端服务。  
- **功能模块**：
  - 知识图谱的查询与管理接口。
  - 测试题目的随机抽取与结果判定接口。
  - 数据库的交互管理。

### 3. 后端数据库（Data）  
- **相关文件存放路径**：`data/` 文件夹  
- **技术选型**：采用 **Neo4j** 图数据库进行存储和管理。  
- **数据内容**：所有知识点和测试题目以 **CSV 文件** 格式存储并导入。  
- **特点**：
  - 知识点与测试题目通过图数据库的关系连接，实现结构化存储。
  - 支持复杂的关系查询和高效的数据检索。

---

## 核心功能实现
1. **知识点展示**：
   - 提供知识图谱视图，展示瀑布模型的各个阶段及其之间的逻辑关系。  
   - 知识点以节点形式显示，用户点击节点可查看详细信息。

2. **随机测试**：
   - 从题库中随机抽取若干题目组成测试。  
   - 用户完成作答后，点击提交，系统即时判分，并反馈正确答案与成绩。  

3. **数据管理**：
   - 数据库采用关系型结构存储，支持高效查询与扩展。

---

## 环境配置
### 前端环境
- Node.js 16.x 或更高版本  
- Vue CLI 4.x  
- 依赖安装：`npm install`

### 后端环境
- JDK 17  
- Spring Boot 3.x  
- 构建工具：Maven  
- 运行命令：`mvn spring-boot:run`

### 数据库环境
- Neo4j 5.x  
- 数据导入工具：Neo4j Browser 或 Cypher Shell  

---

## 使用指南

> 注意要提前配置好环境，Neo4j需要去官网下载桌面版，保证电脑有jdk17及以上；后端需要配置Maven；前端需要配置Vue相关环境，具体如何配置可以询问chatGPT

1. clone整个项目到本地

2. 启动 **Neo4j** 数据库（建议使用桌面版Neo4j），将``/data``文件夹下的csv文件导入数据库的import文件夹中，启动数据库，将同文件夹下的``code.cypher``文件中的内容复制到Neo4j Browser中，完成数据导入。

3. 打开使用java的IDE打开本地的``/api``，配置好maven。运行``api\demo\src\main\java\com\example\Test\TestApplication.java``，启动后端服务。  

4. 使用vscode打开``/Frontend/Waterfall-project``文件夹，在终端中输入

```bash
npm install
npm run dev
```

下载相关依赖后运行（可以使用ctrl+c退出运行）

最后使用浏览器访问http://localhost:5173/端口即可

> 确保查看网页的时候各部分程序都正在运行

## 接口使用说明

> 以下为访问接口需要的url

1.请求所有subject节点和knowledge节点以及关系

http://localhost:8080/knowledge/nodes-and-relationships

2.用id请求节点

http://localhost:8080/knowledge/by_id/1

后面的1可以替换成具体的节点id，每个节点的id可以看csv里面对照

3.用节点名字请求节点

http://localhost:8080/knowledge/by_name/敏捷开发

最后一部分可替换成具体的名字

4.请求题目

http://localhost:8080/knowledge/random-tests?limit=5

最后那个数字是请求的题目数量，可修改
