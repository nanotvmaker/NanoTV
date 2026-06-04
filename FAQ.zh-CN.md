# ❓ 常见问题

在这里您可以找到关于 NanoTV 功能使用的常见问题解答。

> 🇺🇸 [English Version](FAQ.md)

---

## 🎙️ 如何启动实时字幕功能

1. **初始化模型**:
   进入 **设置 - 实时字幕和翻译设置** - 首次启动需要初始化模型，首次初始化需要模型加载和 GPU 编译，大约 1-2 分钟时间，点击 **初始化模型** 开始初始化，耐心等待初始化完成。

2. **启用功能**:
   初始化完成后，点击下面的 **启用实时字幕(英文)** 按钮，显示 On 时，表示已经启动。

3. **使用**:
   启动以后，播放视频时，下滑触摸板菜单会显示 **实时字幕** 按钮，点击按钮开始实时字幕生成。实时字幕只针对英语音频的视频节目进行英文字幕生成，如果要同时显示英文字幕和翻译后的字幕，还需要启动字幕翻译功能。

---

## 🌐 如何启动字幕翻译功能

1. 进入 **设置 - 实时字幕和翻译设置**。

2. 点击启用字幕翻译功能按钮，第一次启动会有一个免责声明提示，确认后才能进行翻译服务配置。

3. 确认后，点击 **翻译服务配置** 按钮，进入配置页面，选择翻译服务。

4. **选择服务**:
   翻译服务目前提供三种方式供选择，都需要验证可用后，才能真正进行实时翻译。

5. **Google / Microsoft**:
   第一和第二种方式分别使用 Google 和 Microsoft 的翻译服务，翻译服务的验证是否成功，取决于网络连接和速度，如果网络不能连通或者速度太慢会影响验证结果。

6. **自定义接口**:
   如果要更灵活的方式或者希望本地部署翻译访问减少翻译时的延迟，可以采用第三种定制接口，定制接口的使用方式请参考下文。

---

<a id="local-translation"></a>

## 🔒 如何使用内置本地翻译（tvOS）

从 **tvOS v1.2.29** 起，NanoTV 可使用内置模型完全在 Apple TV 本地翻译字幕。翻译 **完全在本设备上运行**——不联网，数据不会离开 Apple TV。

**目前仅支持英文作为源语言**（英文 → 简体中文 / 繁体中文）。

### 设置步骤

1. 进入 **设置 - 实时字幕和翻译设置**。
2. 点击 **启用字幕翻译功能**。
3. 进入 **本地翻译** 视图。
4. 选中需要的翻译对，点击 **加载并验证**。

当显示 **服务可用** 后即可使用。播放视频时，打开菜单点击 **翻译** 按钮，选择目标语言即可。

---

<a id="multiple-epg"></a>

## 📺 如何配置多 EPG（逗号分隔）

NanoTV 支持在同一个 EPG 输入框中配置多个节目单地址，使用英文逗号分隔。

### 示例

```text
https://epg1.example.com/guide.xml,https://epg2.example.com/epg.xml,https://epg3.example.com/tv.xml
```

### 使用建议

1. 每个 EPG 地址都应填写完整的 `http://` 或 `https://` 链接。
2. 分隔符请使用 **英文逗号** `,`，不要使用中文逗号 `，`。
3. 建议不要在 URL 前后添加多余空格。
4. 如果某个节目单源暂时不可用，保留其他可用源，仍可提高节目单加载成功率。

---

## 🛠️ 如何添加自定义翻译接口

我们支持兼容 Google Translate API 格式的自托管翻译服务，例如 [MTranServer](https://github.com/xxnuo/MTranServer)。

### 1. 部署翻译模型应用
参考: [**MTranServer on GitHub**](https://github.com/xxnuo/MTranServer?tab=readme-ov-file)

**创建 `docker-compose.yml`**:

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

**启动 Docker**:
```bash
docker compose up -d
```

### 2. 配置 NanoTV
假设部署 Docker 的 IP 地址为：`192.168.1.100`。

进入 **设置 - 实时字幕和翻译设置 - 启用字幕翻译功能 - 翻译服务配置 - 定制接口**:

- **Base URL**: `http://192.168.1.100:8989`
- **Path URL**: `/google/language/translate/v2`
- **认证令牌**: 根据 `docker-compose.yml` 中的配置决定是否填写，如果没有配置则留空。

点击 **验证** 按钮，如果通过，播放视频时，点击菜单上的 **翻译** 按钮选择翻译目标语言后，转录时就可以进行实时翻译。

---

## 🆓 是否有公益的翻译服务？

有的 - 感谢 Linxudo Jacopo 提供的公益翻译服务。

**接入方法**:
打开 NanoTV 进入 **设置** > **实时字幕和翻译** > **翻译服务配置** 窗口，在 **定制接口** 进行配置：

1. **Base URL**: `https://translate.houlang.cloud`
2. **Path URL**: 保持不变
3. **认证令牌**: 不需要输入，留空
4. 点击 **验证**。如果显示服务可用，就可以了。

- **信息来源**: [https://linux.do/t/topic/1616910](https://linux.do/t/topic/1616910)
