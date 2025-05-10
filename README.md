# trss-yunzai-napcat-guide

### 准备材料

1. 已经安装好的 trss-yunzai
2. docker

### 步骤

1. 卸载trss-yunzai的ICQQ-plugin

2. 运行命令

   ```shell
   docker run -d \
       -e NAPCAT_GID=0 \
       -e NAPCAT_UID=0 \
       -p 3000:3000 \
       -p 3001:3001 \
       -p 6099:6099 \
       -v "/root/abys/napcat/QQ:/app/.config/QQ" \ # 这里换成自己的路径
       -v "/root/abys/napcat/config:/app/napcat/config" \ # 这里换成自己的路径
       --add-host=host.docker.internal:host-gateway \
       --name bridge-napcat-docker \
       --restart=unless-stopped \
       mlikiowa/napcat-docker:latest
   ```

3. 查看bridge-napcat-docker容器的控制台， 查找自动生成的token

4. 放行安全组6099端口

5. 访问 http://你的服务器IP:6099/webui

6. 输入token，扫码登录QQ

7. 添加websocket客户端，配置如图

   ```shell
   ws://host.docker.internal:2536/OneBotv11
   ```

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505101908875.png" alt="image-20250510190826779" />

8. 启动登录 trss-yunzai 发现可以正常连上了