---
name: service
description: 整理service里面接口相关信息
---
## 步骤
1. 以service文件为单位，整理出url
2. 根据项目上下文，整理入参、入参，以及什么意思
## 案例
#### `POST /api/bff/student/getStudentList`
- 内容：（学生列表分页/筛选）
- 入参：
  - `pageNo`：页码
  - `pageSize`：每页条数
  - `studentName`：学生姓名关键词
  - `studentNo`：学号
  - `grade`：年级
  - `className`：班级名称
- 出参：
  - `data`：学生列表
  - `paging.pageNo`：当前页码
  - `paging.pageSize`：每页条数
  - `paging.totalHits`：总条数
  - `id`：学生 ID
  - `studentName`：学生姓名
  - `studentNo`：学号
  - `age`：年龄
  - `grade`：年级
  - `className`：班级名称
  - `enrollTime`：入学时间