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
