# trss-yunzai-napcat-guide

> [!TIP]
> miao-yunzai 切换为 trss-yunzai 只需在根目录运行 `node trss.js`，然后重装一下依赖就行

> [!TIP]
> trss-yunzai 设置主人只需对着机器人发送 `#设置主人`，然后回到控制台查看验证码，再把验证码发送给机器人就行

> [!TIP]
> 如果你想切换 napcat 里面登录的 QQ 账号，只需要重启 napcat 就行

## Linux

### 准备材料

1. 已经安装好的 trss-yunzai
2. docker

### 步骤

1. 卸载 trss-yunzai 的 ICQQ-plugin 插件（直接删掉 Yunzai-Bot/plugins/ICQQ-plugin 文件夹）

2. 运行命令，请注意不是在 trss 的 fish 里运行，需要在主机的终端里运行

   ```shell
   docker run -d \
       -e NAPCAT_GID=0 \
       -e NAPCAT_UID=0 \
       -p 3000:3000 \
       -p 3001:3001 \
       -p 6099:6099 \
       # 这里换成自己的路径
       -v "/root/abys/napcat/QQ:/app/.config/QQ" \
       # 这里换成自己的路径
       -v "/root/abys/napcat/config:/app/napcat/config" \
       --add-host=host.docker.internal:host-gateway \
       --name bridge-napcat-docker \
       --restart=unless-stopped \
       mlikiowa/napcat-docker:latest
   ```

3. 放行安全组 6099 端口

4. 访问 http://你的服务器IP:6099/webui

5. 输入 token，~~默认是 `napcat`~~ (新版本需要使用命令 `docker logs --tail 300 bridge-napcat-docker` 查看 token)
   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/a9346128fad4a61f90b688322c052a87.png" alt="image-20250511224351665" style="zoom:33%;" />

6. 扫码登录 QQ ，如果登录不上，请检查 QQ 是否被封禁了

7. 添加 websocket 客户端，配置如图

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112300547.png" alt="image-20250511230042493" style="zoom:33%;" />

   ```shell
   ws://host.docker.internal:2536/OneBotv11
   ```

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/20250731175906.png" alt="image-20250510190826779" style="zoom:33%;" />

8. 启动登录 trss-yunzai 发现可以正常连上了

## Windows

### 准备材料

1. 已经安装好的 trss-yunzai

### 参考资料

https://napneko.github.io/guide/boot/Shell

### 步骤

1. 卸载 trss-yunzai 的 ICQQ-plugin 插件（直接删掉 Yunzai-Bot/plugins/ICQQ-plugin 文件夹）

2. 下载 https://github.com/NapNeko/NapCatQQ/releases/latest/download/NapCat.Shell.Windows.OneKey.zip 并解压 

   > 如果下载不下来可以尝试镜像地址 https://github.moeyy.xyz/https://github.com/NapNeko/NapCatQQ/releases/latest/download/NapCat.Shell.Windows.OneKey.zip

3. 进入文件夹，双击运行 `NapCatInstaller.exe`，会自动下载 QQ 以及相关文件

4. 上一步结束以后，会在当前文件夹生成一个 `NapCat.34740.Shell` 文件夹（中间数字可能会变，但是大概长这样），进入文件夹。

5. 运行文件夹里的 napcat.bat

6. 会自动安装 ffmpeg，如果能正常安装上就行，前面的二维码扫不了也不用管

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112243760.png" alt="image-20250511224351665" style="zoom:33%;" />

   **注意观察命令行里，会展示 token ，复制下来后面要用到**
   
   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/a9346128fad4a61f90b688322c052a87.png" alt="image-20250511224351665" style="zoom:33%;" />

7. 浏览器打开 http://localhost:6099/webui

8. 输入刚刚复制的 token

9. 扫码登录，如果登录不上，请检查 QQ 是否被封禁了

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112245391.png" alt="image-20250511224517335" style="zoom:33%;" />

10. 启动 trss-yunzai

11. 回到浏览器，进入 网络配置 -> 新建 -> Websocket 客户端

   <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112300547.png" alt="image-20250511230042493" style="zoom:33%;" />

12. 具体配置如图

    ```shell
    ws://localhost:2536/OneBotv11
    ```

    <img src="https://raw.githubusercontent.com/bling-yshs/ys-image-host/main/img/202505112247083.png" alt="image-20250511224724028" style="zoom:33%;" />

13. 回到 trss，发现连上了
