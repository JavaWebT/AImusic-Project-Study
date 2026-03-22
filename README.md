# AImusic-Project-Study
记录AImusic从创建到落地的学习总结
## 项目介绍
### P1.项目演示
- 该项目主要实现了AI生成音乐、售卖AI生成音乐服务的功能
-  具体来说，AI生成音乐能够生成纯音乐以及带歌词的音乐。还能够浏览别人创作的音乐，获取其提示词等内容来创作同款。
- 售卖功能，可以指定创作积分以及商品的价格。
### P2.项目介绍，技术栈
- 后端：JDK21、Springboot3.x、Mysql、Redis
- 前端 vue3+element plus+pinia
- 项目业务架构图
<img width="2714" height="1004" alt="业务时序图" src="https://github.com/user-attachments/assets/01d3444e-0559-420f-95d1-d8dfb7d94661" />
- 音乐生成时序图
<img width="2642" height="1266" alt="image" src="https://github.com/user-attachments/assets/c80b87f1-f84f-4d75-8135-123e3449ab86" />
- 支付时序图
<img width="2702" height="1750" alt="image" src="https://github.com/user-attachments/assets/461828ee-fa8b-4288-acb5-c4b90a293099" />

## JAVA后端
### P3代码运行
- 设计用户信息表可以注意的几个点
1. statue 字段，为1，用户能正常使用；为0，该用户被ban掉，是为了防止有些用户恶意攻击我们的应用，比如自己的网站被疯狂访问。
2. last_login_time 字段 ，可以用来统计用户的日活、月活等，准确的说，该字段只能让我们得到每月的登陆人数/某日的登录人数
3. 对于该应用，因为其使用Email作为用户名，所以其应该被设置为 UNIQUE
4. 对于user_id，也要设置为随机生成，避免通过增量生成，导致该应用被恶意攻击
5. 因为前后端分离，所以前端和后端都需要运行起来，
### P4 基础代码生成
1. 通过idea 运行框中的SQL语句能够方便我们排查BUG
2. 一般来说，我们主要写control，其余的根据需求写

### P5 验证码
- 作用：防止人机遍历账号密码
-  逻辑：先写一个control类，具体来说：
-  1. 调用验证码接口，生成验证码对象captcha_A（比如 带计算的图片或者是带数字的图片）
   2. 将验证码转换为文本存入变量 Code，并调用缓存将 Code 转换为一个随机生成的 CodeKey 存起来到缓存中，并为这个 CodeKey 设置了一个过期时间，防止人机爆破
   3. 将captcha 图片转换为base64码base64_captcha_A
   4. 创建一个Vo对象captcha_Vo并将（base64_captcha_A，CodeKey)保存到captcha_Vo中，返回给用户
   5. 因为 CodeKey 与 Code 是对应的，若用户传来一个数字，随后会根据用户的CodeKey来查找缓存中的Code，与其对照，实现功能

### P6注册
- 密码等重要信息不要明文存入数据库，要经过编码，CSDN曾经就用明文存储，导致库被偷了
- 重要的字段通过枚举enums变量来保存，在JAVA中定义类使用的statics 表示可以不需要通过创建相应的类对象就能够调用该方法
- 该项目中的constants为客户端和服务器通用的，所以应该将其放入到common文件夹下
- 因为admin,common,web三个位置代码内容与讲师的不一致，导致后面文件出现冲突。

