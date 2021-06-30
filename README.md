# jd_ql

https://github.com/xtster/jd_qinglong.git

青龙项目指南:

1. 拉取镜像/更新镜像

docker pull whyour/qinglong:latest

2. 删除镜像

docker rmi whyour/qinglong:latest

3. 启动容器 

普通服务器

docker run -dit \
   -v $PWD/ql/config:/ql/config \
   -v $PWD/ql/log:/ql/log \
   -v $PWD/ql/db:/ql/db \
   -p 5700:5700 \
   --name qinglong \
   --hostname qinglong \
   --restart always \
   whyour/qinglong:latest

n1等路由器

docker run -dit \
   -v $PWD/ql/config:/ql/config \
   -v $PWD/ql/log:/ql/log \
   -v $PWD/ql/db:/ql/db \
   --net host \
   --name qinglong \
   --hostname qinglong \
   --restart always \
   whyour/qinglong:latest

4. 删除容器

docker rm -f qinglong

5. 初次登陆

初次访问 http://<自己ip>:5700
使用 admin/adminadmin 登陆，提示已初始化密码
去自己映射目录config下找 auth.json，查看里面的 password
docker exec -it qinglong cat /ql/config/auth.json

6. Cookie管理

登陆成功进入Cookie管理页面，右上角新增Cookie(最新版已加Cookie格式验证)
添加成功，可在Cookie列表更新Cookie，删除Cookie

7. 基本命令

(容器内执行或者新建定时任务时忽略docker exec -it qinglong)

更新青龙
docker exec -it qinglong ql update

更新青龙并编译
docker exec -it qinglong ql restart

拉取自定义仓库
docker exec -it qinglong ql repo https://ghproxy.com/https://github.com/whyour/hundun.git "quanx" "tokens|caiyun|didi|donate|fold|Env"

拉取单个脚本
docker exec -it qinglong ql raw https://ghproxy.com/https://raw.githubusercontent.com/moposmall/Script/main/Me/jx_cfd.js

删除7天前的所有日志
docker exec -it qinglong ql rmlog 7

启动bot
docker exec -it qinglong ql bot

导出互助码
docker exec -it qinglong ql code

通知测试
docker exec -it qinglong notify test test

立即执行脚本
docker exec -it qinglong task test.js now

并行执行脚本
docker exec -it qinglong task test.js conc


三、常用表达式例子

  （1）0 0 2 1 * ? *   表示在每月的1日的凌晨2点调整任务

  （2）0 15 10 ? * MON-FRI   表示周一到周五每天上午10:15执行作业

  （3）0 15 10 ? 6L 2002-2006   表示2002-2006年的每个月的最后一个星期五上午10:15执行作

  （4）0 0 10,14,16 * * ?   每天上午10点，下午2点，4点 

  （5）0 0/30 9-17 * * ?   朝九晚五工作时间内每半小时 

  （6）0 0 12 ? * WED    表示每个星期三中午12点 

  （7）0 0 12 * * ?   每天中午12点触发 

  （8）0 15 10 ? * *    每天上午10:15触发 

  （9）0 15 10 * * ?     每天上午10:15触发 

  （10）0 15 10 * * ? *    每天上午10:15触发 

  （11）0 15 10 * * ? 2005    2005年的每天上午10:15触发 

  （12）0 * 14 * * ?     在每天下午2点到下午2:59期间的每1分钟触发 

  （13）0 0/5 14 * * ?    在每天下午2点到下午2:55期间的每5分钟触发 

  （14）0 0/5 14,18 * * ?     在每天下午2点到2:55期间和下午6点到6:55期间的每5分钟触发 

  （15）0 0-5 14 * * ?    在每天下午2点到下午2:05期间的每1分钟触发 

  （16）0 10,44 14 ? 3 WED    每年三月的星期三的下午2:10和2:44触发 

  （17）0 15 10 ? * MON-FRI    周一至周五的上午10:15触发 

  （18）0 15 10 15 * ?    每月15日上午10:15触发 

  （19）0 15 10 L * ?    每月最后一日的上午10:15触发 

  （20）0 15 10 ? * 6L    每月的最后一个星期五上午10:15触发 

  （21）0 15 10 ? * 6L 2002-2005   2002年至2005年的每月的最后一个星期五上午10:15触发 

  （22）0 15 10 ? * 6#3   每月的第三个星期五上午10:15触发
