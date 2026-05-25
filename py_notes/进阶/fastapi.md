# FastAPI 是什么
FastAPI = Python 现代后端框架
核心特点：
⚡ 非常快（基于 Starlette + Pydantic）
🧠 自动参数校验
📄 自动生成接口文档（Swagger / ReDoc）
🧩 非常适合做微服务 / API项目

# 启动FastApi                         uvicorn main:app --reload --port 8000    (pycharm终端执行, 项目根目录)
                                      uvicorn main:app --reload          
# 查看端口占用                         netstat -ano | findstr 8000
# 清除进程                             taskkill /PID 号码 /F
# 停止所有python.exe                   taskkill /IM python.exe /F     (适用于进程卡死)

# 什么是Pydantic模型
Pydantic模型 = 用来定义和校验数据结构的“数据模板”

# 什么是Field
Field 是给 Pydantic字段添加“额外规则和描述”的工具。
你可以理解成： 👉 “字段的配置器”

# 分层思想
① Router层（接口层） 负责： 接收请求 返回响应
                    不负责： SQL 业务逻辑
② Service层（业务层） 负责： 查询数据库 核心业务逻辑
③ Schema层（数据模型层） 负责： 参数校验 请求体定义
④ Database层 负责： 数据库连接

# ORM = Object Relational Mapping
对象关系映射
简单理解：
数据库	Python
表	    类
行数据	对象
字段	    属性

# flush vs commit
db.flush()
作用： 同步SQL到数据库 但还没真正提交 还能 rollback。

db.commit()
作用： 真正永久保存

# Depends（依赖注入）
核心思想： “把公共逻辑抽出来自动复用”

# yield db
👉 “先把db交出去用” , 等接口执行结束后：
finally:
    db.close() 自动执行。
这就是 FastAPI 自动资源管理

# 响应模型
作用：控制“返回给前端的数据”

# orm_mode 是什么
因为返回的是ORM对象,不是dict。
加： orm_mode = True ,Pydantic才能读取： user.username 这种ORM属性。

# “你项目JWT用什么实现的？”
你可以回答：
Flask项目里使用的是PyJWT，
FastAPI项目里使用的是python-jose，
本质都是JWT签发和验证，
只是生态里常见选择不同。

# 什么是 中间件 Middleware ?
中间件：
请求 -> 中间件 -> 路由
响应 <- 中间件 <- 路由
所有请求都会先经过它。
## 中间件执行顺序（重要）
请求 -> Middleware -> Router -> Service

响应 <- Middleware <- Router <- Service

# 异步函数 async
async def
    await

await 表示这里需要等待, 但等待期间可以去干别的事async def

# 中间件和 Depends区别（重点）
Depends 针对某个接口 比如：Depends(get_current_user)
Middleware 针对所有请求

# Formatter
决定： 日志长什么样
# Handler
决定： 日志输出到哪里

# split(".")
这是 Python 字符串切割

#  StaticFile
FastAPI 的静态文件服务类
作用： 让浏览器能够访问： 图片 css js 上传文件 静态资源

# Alembic
专门管理数据库版本

# ORM 负责： 定义数据结构
# Alembic 负责： 同步数据库结构

# 生成迁移(给数据库表添加字段)
alembic revision --autogenerate -m "add 字段名"
    升级字段 alembic revision --autogenerate -m "fix 字段名 新增参数"
# 执行迁移
alembic upgrade head

# .env 是什么？
相当于：项目环境变量文件

# from typing import Optional
它的意思是： ✅ “这个值可以是某种类型，也可以是 None”，例如 Optional[str] 表示可以为str或空

# UploadFile 不能直接放进 Pydantic 模型 所以 FastAPI 提供：from fastapi import Form 用于接收： form-data中的普通字段

# ge 是：✅ greater than or equal
意思： “大于等于”

# order_by 和 sort
order_by 按什么字段排序： id username email
sort 排序方向： asc desc
# 排序方向：asc desc
✅ asc 全称： ascending 意思： 升序 
🚀 升序效果
数字： 1 2 3 4 5 字母： a b c d 时间： 旧 -> 新
✅ desc 全称： descending 意思： 降序
🚀 降序效果
数字： 5 4 3 2 1 字母： z y x 时间： 新 -> 旧

# 排序字段白名单校验
企业项目里非常重要。 作用： 防止前端乱传字段导致程序报错

# 接口语义
return user 表示： 返回业务数据
return True/False 表示： 返回操作状态

# 软删除核心思想
不是： DELETE FROM users 而是： UPDATE users SET is_deleted = 1
🚀 数据还在数据库 只是： 查询时不显示

# 在 MySQL 里：Boolean 本质上其实是： TINYINT(1)
所以： 
Python	MySQL存储
True	1
False	0

# 一句话区别
类型	            作用
HTTPException	抛异常
JSONResponse	手动返回响应

# 企业项目常见 code 设计（了解）
code	含义
200	    成功
400	    参数错误
401	    未登录
403	    无权限
404	    数据不存在
500	    服务器错误

# RBAC
Role-Based Access Control
基于角色的权限控制。

# bcrypt 是什么？
企业最常用密码加密算法之一。
特点：
✅ 自动加盐
✅ 很难破解
✅ 同样密码每次结果不同
✅ 专门用于密码存储

# 为什么企业不会允许超长密码？
极长密码：
❌ 容易攻击服务器
❌ bcrypt计算更慢
❌ 没实际意义

# 为什么需要 Refresh Token？
如果只有： access_token 过期后： ❌ 用户必须重新登录
而 Refresh Token： 可以： ✅ 自动续期 用户几乎无感。

# Redis 是什么？
Redis： 内存数据库
特性	        描述
超快	        基于内存
支持缓存	    最常见用途
支持过期时间	token/session
支持高并发	企业核心组件
# 为什么需要 Redis？
现在每次请求： 都查 MySQL 如果用户很多： ❌ 数据库压力巨大
所以企业项目一定会： ✅ 缓存热点数据 
🚀 Redis 就是最常用缓存中间件。
# Redis 最常见用途（重要）
缓存用户信息 减少数据库查询。 
token存储 JWT黑名单。
验证码 短信验证码。
排行榜 游戏/热搜。
限流 防刷接口。

# 缓存当前用户信息前为什么要import json
Redis 不能直接存 Python 的 dict, 所以需要转成 JSON 字符串
方法	            作用
json.dumps()	dict → JSON字符串
json.loads()	JSON字符串 → dict

# 3️⃣ 为什么企业喜欢删除缓存？（重点）
因为： 更新缓存很复杂 比如： 你有： 用户缓存 用户列表缓存 管理员缓存
你根本不知道： 要更新多少缓存
所以企业通常： ✅ 直接删缓存 下次查询： 自动重新加载。
🚀 简单稳定

# 修改密码需要删缓存吗？（了解）
通常： 不需要
因为： 缓存里一般不存密码