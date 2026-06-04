# ❓ FAQ

Here you can find answers to common questions about using NanoTV features.

> 🇨🇳 [简体中文版](FAQ.zh-CN.md)

---

## 🎙️ How to enable Real-time Subtitles

1. **Initialize Model**:
   Go to **Settings - Real-time Subtitle & Translation**. The first launch requires model initialization (loading & GPU compilation), which takes about 1-2 minutes. Click **Initialize Model** and wait patiently.

2. **Enable Feature**:
   After initialization, toggle the **Enable Real-time Subtitles (English)** switch. "On" means it is active.

3. **Usage**:
   During video playback, swipe down on the remote touchpad to open the menu. You will see a **Real-time Subtitles** button. Click it to start generation.
   *Note: Real-time subtitles currently support English audio only. To see translated subtitles, you need to enable the Translation feature as well.*

---

## 🌐 How to enable Subtitle Translation

1. Go to **Settings - Real-time Subtitle & Translation**.

2. Toggle **Enable Subtitle Translation**. A disclaimer will appear on first use; confirm to proceed to configuration.

3. Click **Translation Service Configuration** to select a provider.

4. **Select Provider**:
   Currently, three methods are supported. Each must be verified before use.

5. **Google / Microsoft**:
   The first two options use Google and Microsoft translation services respectively. Success depends on your network connection.

6. **Custom API**:
   For more flexibility or lower latency (local deployment), use the third option "Custom API". See below for details.

---

<a id="local-translation"></a>

## 🔒 How to use Built-in On-Device Translation (tvOS)

Starting with **tvOS v1.2.29**, NanoTV can translate subtitles entirely on your Apple TV using a bundled model. Translation runs **100% on-device** — no network connection is used and no data ever leaves your Apple TV.

**Currently supports English as the source language only** (English → Simplified Chinese / Traditional Chinese).

### Setup steps

1. Go to **Settings - Real-time Subtitle & Translation**.
2. Toggle **Enable Subtitle Translation**.
3. Open the **Local Translation** view.
4. Select the translation pair you need, then tap **Load & Validate**.

Once it shows **Service Available**, the pair is ready. During playback, open the menu, tap **Translate**, and choose your target language.

---

<a id="multiple-epg"></a>

## 📺 How to configure multiple EPG URLs (comma-separated)

NanoTV supports entering multiple EPG sources in one input field, separated by commas.

### Example

```text
https://epg1.example.com/guide.xml,https://epg2.example.com/epg.xml,https://epg3.example.com/tv.xml
```

### Tips

1. Use full `http://` or `https://` URLs for each EPG source.
2. Use **English commas** `,` as separators, and do not use Chinese commas `，`.
3. Do not add extra spaces before/after URLs where possible.
4. If one source is temporarily unavailable, keep other valid sources so guide loading can still succeed.

---

## 🛠️ How to add Custom Translation API

We support self-hosted translation services compatible with Google Translate API format, such as [MTranServer](https://github.com/xxnuo/MTranServer).

### 1. Deploy Translation Service
Reference: [**MTranServer on GitHub**](https://github.com/xxnuo/MTranServer?tab=readme-ov-file)

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

**Start Docker**:
```bash
docker compose up -d
```

### 2. Configure NanoTV
Assuming your Docker host IP is `192.168.1.100`.

Go to **Settings - Real-time Subtitle & Translation - Translation Service Configuration - Custom API**:

- **Base URL**: `http://192.168.1.100:8989`
- **Path URL**: `/google/language/translate/v2`
- **Auth Token**: Configure this only if you set `CORE_API_TOKEN` in `docker-compose.yml`. Otherwise, leave blank.

Click **Verify**. If successful, you can now use real-time translation during playback by selecting your target language in the **Translate** menu.

---

## 🆓 Is there a free/public translation service?

Yes - Thanks to Linxudo Jacopo for providing the public interest translation service.

**Setup Method**:
Open NanoTV, go to **Settings > Real-time Subtitle & Translation > Translation Service Configuration**, and configure the **Custom API**:

1. **Base URL**: `https://translate.houlang.cloud`
2. **Path URL**: Keep default
3. **Auth Token**: Leave blank
4. Click **Verify**. If it shows service available, you are all set.

- **Source**: [https://linux.do/t/topic/1616910](https://linux.do/t/topic/1616910)
