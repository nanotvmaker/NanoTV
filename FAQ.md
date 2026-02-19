# ❓ FAQ / 常见问题

Here you can find answers to common questions about using NanoTV features.
在这里您可以找到关于 NanoTV 功能使用的常见问题解答。

---

## 🎙️ How to enable Real-time Subtitles / 如何启动实时字幕功能

1. **Initialize Model / 初始化模型**:
   Go to **Settings - Real-time Subtitle & Translation** (**设置 - 实时字幕和翻译设置**). The first launch requires model initialization (loading & GPU compilation), which takes about 1-2 minutes. Click **Initialize Model** and wait patiently.
   进入 **设置 - 实时字幕和翻译设置** - 首次启动需要初始化模型，首次初始化需要模型加载和GPU编译，大约1-2分钟时间，点击**初始化模型**开始初始化，耐心等待初始化完成。

2. **Enable Feature / 启用功能**:
   After initialization, toggle the **Enable Real-time Subtitles (English)** switch. "On" means it is active.
   初始化完成后，点击下面的 **启用实时字幕(英文)** 按钮，显示 On 时，表示已经启动。

3. **Usage / 使用**:
   During video playback, swipe down on the remote touchpad to open the menu. You will see a **Real-time Subtitles** button. Click it to start generation.
   *Note: Real-time subtitles currently support English audio only. To see translated subtitles, you need to enable the Translation feature as well.*
   启动以后，如果播放视频时，下滑触摸板菜单会显示**实时字幕**按钮，点击按钮开始实时字幕生成。 实时字幕只针对英语音频的视频节目进行英文字幕生成，如果要同时显示英文字幕和翻译后的字幕，还需要启动字幕翻译功能。

---

## 🌐 How to enable Subtitle Translation / 如何启动字幕翻译功能

1. Go to **Settings - Real-time Subtitle & Translation** (**设置 - 实时字幕和翻译设置**).
   进入 **设置 - 实时字幕和翻译设置**。

2. Toggle **Enable Subtitle Translation**. A disclaimer will appear on first use; confirm to proceed to configuration.
   点击启用字幕翻译功能按钮，第一次启动会有一个免责声明提示，确认后才能进行翻译服务配置。

3. Click **Translation Service Configuration** to select a provider.
   确认后，点击 **翻译服务配置** 按钮，进入配置页面，选择翻译服务。

4. **Select Provider / 选择服务**:
   Currently, three methods are supported. Each must be verified before use.
   翻译服务目前提供三种方式供选择，都需要验证可用后，才能真正进行实时翻译。

5. **Google / Microsoft**:
   The first two options use Google and Microsoft translation services respectively. Success depends on your network connection.
   第一和第二种方式分别使用Google 和 Microsoft 的翻译服务，翻译服务的验证是否成功，取决于网络连接和速度，如果网络不能连通或者速度太慢会影响验证结果。

6. **Custom API / 自定义接口**:
   For more flexibility or lower latency (local deployment), use the third option "Custom API". See below for details.
   如果要更灵活的方式或者希望本地部署翻译访问减少翻译时的延迟，可以采用第三种定制接口，定制接口的使用方式请参考下文。

---

## 🛠️ How to add Custom Translation API / 如何添加自定义翻译接口

We support self-hosted translation services compatible with Google Translate API format, such as [MTranServer](https://github.com/xxnuo/MTranServer).
我们支持兼容 Google Translate API 格式的自托管翻译服务，例如 [MTranServer](https://github.com/xxnuo/MTranServer)。

### 1. Deploy Translation Service / 部署翻译模型应用
Reference / 参考: [**MTranServer on GitHub**](https://github.com/xxnuo/MTranServer?tab=readme-ov-file)

**Create `docker-compose.yml`**:

```yaml
services:
  mtranserver:
    image: xxnuo/mtranserver:latest
    container_name: mtranserver
    restart: unless-stopped
    ports:
      - "8989:8989"
    volumes:
      - ./models:/app/models
    environment:
      # - CORE_API_TOKEN=your_token
```

**Start Docker / 启动 Docker**:
```bash
docker compose up -d
```

### 2. Configure NanoTV / 配置 NanoTV
Assuming your Docker host IP is `192.168.1.100`.
假设部署 Docker 的 IP 地址为：`192.168.1.100`。

Go to **Settings - Real-time Subtitle & Translation - Translation Service Configuration - Custom API**:
进入 **设置 - 实时字幕和翻译设置 - 启用字幕翻译功能 - 翻译服务配置 - 定制接口**:

- **Base URL**: `http://192.168.1.100:8989`
- **Path URL**: `/google/language/translate/v2`
- **Auth Token / 认证令牌**: Configure this only if you set `CORE_API_TOKEN` in `docker-compose.yml`. Otherwise, leave blank. (根据 `docker-compose.yml` 中的配置，如果没有配置则留空)。

Click **Verify / 验证**. If successful, you can now use real-time translation during playback by selecting your target language in the **Translate** menu.
点击 **验证** 按钮，如果通过，播放视频时，点击菜单上的 **翻译** 按钮选择翻译目标语言后，转录时就可以进行实时翻译。

---

## 🆓 Is there a free/public translation service? / 是否有公益的翻译服务？

Yes - Thanks to Linxudo Jacopo for providing the public interest translation service.
有的 - 感谢 Linxudo Jacopo 提供的公益翻译服务。

**Setup Method / 接入方法**:
Open NanoTV, go to **Settings > Real-time Subtitle & Translation > Translation Service Configuration**, and configure the **Custom API**:
打开 NanoTV 进入 **设置** > **实时字幕和翻译** > **翻译服务配置** 窗口，在 **定制接口** 进行配置：

1. **Base URL**: `https://translate.houlang.cloud`
2. **Path URL**: Keep default / 保持不变
3. **Auth Token / 认证令牌**: Leave blank / 不需要输入，留空
4. Click **Verify / 点击验证**. If it shows service available, you are all set. / 如果显示服务可用，就可以了。

- **Source / 信息来源**: [https://linux.do/t/topic/1616910](https://linux.do/t/topic/1616910)
