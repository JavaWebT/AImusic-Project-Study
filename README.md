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
2. last_login_time 字段 ，可以用来统计用户的日活、月活等，具体来说，通过用户每天的字段与日期是否相同，能得到日活，统计该月份该字段的个数，能得到月活
3. 对于该应用，因为其使用Email作为用户名，所以其应该被设置为 UNIQUE
4. 对于user_id，也要设置为随机生成，避免通过增量生成，导致该应用被恶意攻击
### P4 基础代码生成
1. 通过idea 运行框中的SQL语句能够方便我们排查BUG
