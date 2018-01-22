# 基于HTML5的实时聊天工具的设计与实现

## 运行环境：

| 运行环境 | 技术 |
|-----:|:----------|
| 系统环境 | Linux/Mac OS/Windows | 
| 服务器 |  nodejs |
| 数据库 |  mongodb/mysql |


| gulp插件 | 作用 |
|----: |:--------|
| gulp-sass | sass文件编译 |
| gulp-minify-css | css文件压缩 |
| gulp-jshint | js语法检查 | 
| jshint-stylish | js语法检查显示样式 | 
| gulp-uglify | js文件压缩 | 
| gulp-concat | 文件合并 | 
| gulp-rename | 文件重命名 |
| gulp-imagemin | 图片压缩 | 




## 功能模块：
1.用户登录/注册模块

| 名称 | 功能 | 
| ----: | :---- |
| 用户登录 | 实现用户登录 |
| 用户注册 | 实现用户注册 |
| 用户密码找回 | 实现密码找回 |

2.用户个人信息管理模块

| 名称 | 功能 | 
| ----: | :---- |
| 个人信息查看 | 用户或好友对个人信息的查看 | 
| 个人信息修改 | 用户对个人信息的修改(如,昵称、头像、生日等) |
| 密码修改 | 用户登录密码的修改 | 

3.消息模块

| 名称 | 功能 |
| ----: | :---- |
| 一对一消息收发 | 实现用户间一对一的消息收发(包括,文字、表情、图片)|
| 群组消息收发 | 实现群组内消息的收发(包括,文字、表情、图片等) |

4.文件收发模块（非图片的其他文件）

| 名称 | 功能 | 
| ----: | :---- |
| 文件上传 | 实现文件的上传,并临时存储在服务器 |
| 文件下载 | 实现文件的下载 |

5.好友管理

| 名称 | 功能 |
| ----: | :---- |
| 添加好友 | 通过用户账户查找并添加好友 |
| 删除好友 | 对已添加的好友进行删除,并不再收取相应消息 |
| 好友分组 | 对好友进行分组(自定义分组名)|

6.群组创建/解散模块

| 名称 | 功能 |
| ----: | :---- |
| 群组创建 | 实现创建群组(创建者即为管理员) |
| 群组解散 | 创建者有权利解散群组 |

7.加入/退出群组

| 名称 | 功能 |
| ----: | :---- |
| 加入群组 | 用户通过群号申请加入群组 | 
| 踢出群组 | 群管理员将群成员踢出群群组(强制退出)|
| 退出群组 | 用户主动退出群组 | 

## 安装数据库

1. 安装mysql 

2. 设置用户，默认账户：root，密码：123456
> 或在`routes\connection\mysqlPool.js`中修改

3. 创建数据库`create database HTML5Chat;`

4. `use HTML5Chat`

5. 导入数据`source yourPath\HTML5Chat.sql`

6. 添加触发器

```sql
DELIMITER $$

CREATE 
	TRIGGER `HTML5Chat`.`chat_group_AFTER_INSERT` AFTER INSERT 
	ON `chat_group` 
	FOR EACH ROW BEGIN
		INSERT INTO chat_groupUser(groupId,userId,role) VALUE(new.groupId,new.create_by,0); 
	END$$

CREATE
    TRIGGER `HTML5Chat`.`insert_into_login` AFTER INSERT
    ON `HTML5Chat`.`chat_login`
    FOR EACH ROW BEGIN
	INSERT INTO chat_info(id,nickName,picture) VALUE(new.id,new.loginName,DEFAULT); 
	INSERT INTO chat_friendSet(userId,setName,isDefault) VALUE(new.id,DEFAULT,0); 
    END$$

DELIMITER ;
```

## 运行方式：

1. 克隆仓库
```
git clone https://github.com/vu-ji/h5Chat.git
```

2. 安装nodejs环境

地址：[http://nodejs.cn](http://nodejs.cn)

3. 全局安装gulp
```
npm install --global gulp
```

4. 安装node_modules
```
cd h5Chat && npm install
```

5. 运行项目
```
npm start
```

6. 查看运行结果

地址：[http://localhost:3000](http://localhost:3000)






