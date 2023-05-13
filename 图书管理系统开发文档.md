# 图书管理系统开发

摘要：这是一份图书管理系统开发指南

## 开发规格书

1. 用户分类及主要功能：

   1. 图书
      1. 图书的信息管理
      
      2. 图书的导入导出
      
      3. 图书推荐
      
      4. 图书点赞、评论
      
         
      
   2. 读者
      1. 读者注册与注销
      2. 读者登录
      3. 图书借阅与归还
      4. 图书评论
      5. 超时罚款
      
   3. 老师
      1. 管理图书
         1. 维护图书信息
            1. 图书上新
            2. 图书推荐
            3. 修改图书信息
         2. 维护图书评论
            1. 删除评论
      2. 管理读者
         1. 维护读者信息
            1. 修改密码
            2. 修改读者状态
      3. 发布通知公告
      
   4. 超级管理员
      1. 管理图书
      2. 管理读者
      3. 管理老师
   
   开发时间限制：2个月
   
   ## 开发工具与技术
   
   开发方式：web前后端分离开发+微信小程序开发
   
   工具：
   
   	1. 后端：
   		1. mysql
   		2. java
   		3. spring boot
   		4. redis
   		5. rabbitmq
   	2. 前端：
   		1. html+css+js
   		2. elementUI
   		3. vue
   		4. nginx
   	3. 微信小程序：
   		1. 待协商

## 数据库设计
在数据库表的设计中，不建议使用外键。

图书表：t_books

|      名称       | 类型  | 主键 | 外键 | 说明 |
| :--: | :--: |  :--:  | :--: | :--: |
|      id       | int  |      |      | 自增 |
|    book_id    |      |      |      | 图书id |
|   book_name   |      |      |      | 图书名称 |
|  book_cover   |      |      |      | 图书封面 |
|   book_desc   |      |      |      | 图书描述 |
|  book_author  |      |      |      | 图书作者 |
| book_comment  |      |      |      | 图书评论 |
|  book_price   |      |      |      | 图书价格 |
| book_location |      |      |      | 图书位置 |
|  created_by   |      |      |      | 图书创建者 |
| book_likes | | |  | 好评数 |
| book_unlikes | | | | 差评数 |
| book_borrowable | | | | 是否可借阅 |
| book_category | | | | 图书类别 |
| book_borrowtimes | | | | 图书类别 |

图书评论表：
t_comment

|      名称       | 类型  | 主键 | 外键 | 说明 |
| :--: | :--: |  :--:  | :--: | :--: |
|      id       | int  |      |      | 自增 |
|    comment_id    |      | y |      | 图书id |
|   book_id   | varchar |      |      | 用户id |
| user_Id | varchar |      |      | 图书评论 |
|   comment_time   | date |      |      | 图书描述 |
| comment_content | varchar(255) |      |      | 图书评论 |
| is_validation |              |      |      | 评论是否有效 |
|                 |              |      |      |          |



图书推荐表：t_recommend:

|      名称      | 类型 | 主键 | 外键 |   说明   |
| :------------: | :--: | :--: | :--: | :------: |
|       id       | int  |      |      |   自增   |
|                |      |      |      |          |
|    book_id     |      |      |      |          |
| recommend_desc |      |      |      | 推荐描述 |
|   create_by    |      |      |      |  创建者  |
| is_validation  |      |      |      | 是否有效 |
|                |      |      |      |          |



用户表：t_uses

|      名称       | 类型 | 主键 | 外键 |   说明   |
| :-------------: | :--: | :--: | :--: | :------: |
|       id        | int  |      |      |   自增   |
|     user_id     |      |      |      |  用户id  |
|  user_libcard   |      |      |      | 借阅证号 |
|    user_name    |      |      |      | 用户姓名 |
|   user_gender   |      |      |      | 用户性别 |
| user_validation |      |      |  是  | 用户状态 |
|   user_status   |      |      |  是  | 用户身份 |
|  user_password  |      |      |      | 用户密码 |
|                 |      |      |      |          |
|                 |      |      |      |          |
|                 |      |      |      |          |
|                 |      |      |      |          |
|                 |      |      |      |          |

借阅表：t_record_borrow

|     名称      | 类型 | 主键 | 外键 |     说明     |
| :-----------: | :--: | :--: | :--: | :----------: |
|      id       | int  |      |      |     自增     |
|   borrow_id   | int  |      |      |     自增     |
|    book_id    |      |      |      |    用户id    |
|    user_id    |      |      |      |   借阅证号   |
|     sdate     |      |      |      | 借阅开始时间 |
|     edate     |      |      |      | 借阅结束时间 |
|  user_status  |      |      |      |   用户身份   |
| borrow_status |      |      |      |   借阅状态   |



教师表：t_teacher

管理员表：t_admins



身份表t_status：

| 名称 | 类型 | 主键 | 外键 | 说明 |
| :--: | :--: | :--: | :--: | :--: |
|  id  | int  |      |      | 自增 |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |
|      |      |      |      |      |