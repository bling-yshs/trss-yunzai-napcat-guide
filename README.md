# trss-yunzai-napcat-guide

## Linux

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

4. 放行安全组6099端口

5. 访问 http://你的服务器IP:6099/webui

6. 输入token，默认是 `napcat` ，扫码登录QQ

7. 添加websocket客户端，配置如图

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112300547.png" alt="image-20250511230042493" style="zoom:33%;" />

   ```shell
   ws://host.docker.internal:2536/OneBotv11
   ```

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505101908875.png" alt="image-20250510190826779" style="zoom:33%;" />

8. 启动登录 trss-yunzai 发现可以正常连上了

## Windows

### 准备材料

1. 已经安装好的 trss-yunzai
2. 已经安装好的 QQNT（新版QQ）

### 参考资料

https://napneko.github.io/guide/boot/Shell

### 步骤

1. 卸载trss-yunzai的ICQQ-plugin

2. 下载 https://github.com/NapNeko/NapCatQQ/releases/latest/download/NapCat.Shell.Windows.OneKey.zip 并解压

3. 进入文件夹，运行launcher.bat，如果是win10就运行launcher-win10.bat

4. 会自动安装ffmpeg，如果能正常安装上就行，前面的二维码扫不了也不用管

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112243760.png" alt="image-20250511224351665" style="zoom:33%;" />

5. 浏览器打开 http://localhost:6099/webui 默认token是 `napcat`

6. 扫码登录

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112245391.png" alt="image-20250511224517335" style="zoom:33%;" />

7. 启动 trss-yunzai

8. 回到浏览器，进入 网络配置 -> 新建 -> Websocket客户端

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112300547.png" alt="image-20250511230042493" style="zoom:33%;" />

9. 具体配置如图

   ```shell
   ws://localhost:2536/OneBotv11
   ```

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112247083.png" alt="image-20250511224724028" style="zoom:33%;" />

10. 回到trss，发现连上了