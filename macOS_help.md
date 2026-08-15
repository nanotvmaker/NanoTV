# nanoTV macOS Help

Welcome to nanoTV for macOS. This guide covers everything from adding your first subscription to AI subtitles, playback quality and keyboard shortcuts.

> 🇨🇳 [简体中文版](macOS_help.zh-CN.md) · 📱 iOS and tvOS guides: [nanotv.app/support.html](https://nanotv.app/support.html)

---

## 🚀 Quick Start

- **Add your first subscription**: Click the **Add** button on the home page → enter a Subscription Name and URL → click **Add** to submit.
- **Browse & play channels**: Click **Subscriptions** in the sidebar (or press <kbd>⌘2</kbd>) → double-click a channel or click the Play button.
- **Quick channel access**: Press <kbd>⌃1</kbd> – <kbd>⌃5</kbd> to instantly play any of your 5 most recently watched channels.
- **Play any link instantly**: Press <kbd>⌘N</kbd> (or use the quick entry at the bottom of the sidebar), paste a URL and play it right away.

---

## 🤖 AI & Subtitle Features

- **Initialize the model**: Go to **Settings → Subtitles** and click **Initialize Model**. The first run takes about 1–2 minutes for loading and GPU compilation.
- **Enable real-time subtitles**: Toggle **Start Real-time Subtitles** after initialization. During playback, press <kbd>⌃T</kbd> or click the subtitle button at the bottom of the screen.
- **Languages**: Live transcription supports **English**, **Chinese (Mandarin)** and **Japanese**.
- **Translation service**: Choose **Apple on-device translation**, **DeepL**, **large language models (LLM)**, **Google** or **Microsoft** in **Settings → Subtitles & Translation**. A free public service and self-hosted APIs are also supported — see the [FAQ](FAQ.md).
- **Subtitle look**: Pick a frosted-glass or feathered (dark cloud) background, and let the font size adapt automatically to the player window — helpful on large 4K displays.
- **EPG auto-translation**: Enable **EPG Translation** in **Settings → EPG** to auto-translate English program guides to Chinese.

---

## 🎞 Playback & Picture Quality

- **1080i 50p deinterlacing**: Turn on **Settings → Playback Settings → 1080i 50p** to convert 1080i 25fps interlaced video into 50p double-frame-rate output — noticeably smoother for sports and live news.
- **Live buffer**: Adjust the IPTV live buffer in **Settings → Playback Settings**. A larger buffer means fewer stalls; a smaller one means lower live latency.
- **Fast HLS start-up**: Enable **Settings → Fast HLS Start-up** for a quicker playback start on HLS streams.
- **Formats**: 4K/8K playback, MMTP/TLV streams, AV3A audio decoding and refined SDR color rendering are supported out of the box.
- **On-demand programs**: VOD content has a progress bar — drag to seek, or fast-forward and rewind.

---

## 🔍 Search & Program Guide

- **Search everything**: Press <kbd>⇧⌘F</kbd> to search channels and EPG programs across all subscriptions at once. Wrap a term in double quotes `""` for an exact match. Recent searches are kept as history.
- **Zoom the guide**: Zoom the EPG grid in and out to see a wider time range or more channels at once.
- **Keep the guide fresh**: Turn on **Settings → Program Guide → Update EPG when refreshing subscriptions**, or refresh the EPG manually at any time.

---

## 📺 Subscriptions & Layout

- **Text Import**: When adding a subscription, choose **Text Import** and paste one or more plain URLs — ideal for single channels and link-only sources.
- **Auto refresh**: Enable auto-refresh when adding or editing a subscription so your channel list is current at launch.
- **Xtream Codes**: XC sources are detected and filled in automatically. Refresh an existing XC subscription once to apply the improved group ordering.
- **Card columns**: Subscription, favorites and search views use adaptive grids — set how many channel cards appear per row to suit your window size.
- **Proxy & User-Agent**: SOCKS5 and HTTP proxies live in **Settings → Network**; User-Agent can be set per subscription.

---

## ⚡ Quick Play & Favorites

- **Quick Play**: Press <kbd>⌘N</kbd> — or use the entry at the bottom of the sidebar — paste a link and play it immediately. A channel name is optional but makes the entry easier to recognize later.
- **Save as subscription**: Any quick-play history entry can be added as a subscription in one step.
- **Favorites stay put**: Start playback from a favorite and the channel list and channel switching stay inside your favorites. Favorites are also reachable from the guide sidebar (**Subscriptions & Favorites**) and the in-player channel list.

---

## ☁️ iCloud Sync

- **Enable sync**: Go to **Settings → iCloud** and toggle **iCloud Sync** on.
- Automatically syncs **subscriptions** and **favorites** across all your Apple devices (macOS, iOS, tvOS).
- Requires the same Apple ID signed in with iCloud available on all devices.
- The sync log keeps the last 7 days and cleans up expired entries automatically.

---

## ⌨️ Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| **Home** | <kbd>⌘1</kbd> |
| **Subscriptions** | <kbd>⌘2</kbd> |
| **Favorites** | <kbd>⌘3</kbd> |
| **Program Guide (EPG)** | <kbd>⌘4</kbd> |
| **Settings** | <kbd>⌘,</kbd> |
| **Search Channels** | <kbd>⇧⌘F</kbd> |
| **Quick Play (paste a link)** | <kbd>⌘N</kbd> |
| **Play / Pause** | <kbd>⌃P</kbd> |
| **Toggle Real-time Subtitles** | <kbd>⌃T</kbd> |
| **Refresh All Subscriptions** | <kbd>⇧⌘R</kbd> |
| **Quick Play (Recent Channel 1–5)** | <kbd>⌃1</kbd> – <kbd>⌃5</kbd> |

---

For more help, see the [FAQ](FAQ.md), visit [nanotv.app](https://nanotv.app) or join the [Telegram Community](https://t.me/nanotvinfo).
