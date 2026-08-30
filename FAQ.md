# ❓ FAQ

Answers to common questions about nanoTV features.

> 🇨🇳 [简体中文版](FAQ.zh-CN.md) · 📖 Platform guide: [nanotv.app/support.html](https://nanotv.app/support.html)

<!-- Generated from the nanoTV app FAQ source by tools/build-faq-md.mjs in the website repo. Do not edit by hand. -->

---

## Contents

- **📥 Subscriptions & Setup**
  - [How do I add a subscription?](#add-subscription)
  - [How do I import a subscription from Telegram, a web page or an HTTPS link?](#external-subscription-import)
  - [How does automatic refresh work?](#subscription-refresh)
  - [Can I play a single address without creating a subscription?](#quick-play)
  - [Can another app, a web page or Finder hand a video to nanoTV?](#external-playback)
- **📺 Channels & Organizing**
  - [How do I find a channel or program quickly?](#app-search)
  - [How do favorites work?](#favorites)
  - [What are channel tags for?](#channel-tags)
- **📋 Program Guide**
  - [How do I set up the program guide (EPG)?](#epg-setup)
  - [Why do some channels have no guide data?](#epg-missing)
  - [How do program reminders work?](#epg-reminders)
- **💬 Subtitles & Translation**
  - [How do I turn on live transcription (AI subtitles)?](#transcription)
  - [How do I turn on subtitle translation?](#translation)
  - [How do I set up DeepL or LLM translation?](#translation-deepl-llm)
  - [How do I connect my own translation API?](#translation-custom-api)
  - [Is there a free public translation service I can use without hosting one?](#free-translation)
- **🎞 Playback & Picture**
  - [A channel will not play — what now?](#playback-failed)
  - [Live streams keep stuttering — what can I tune?](#live-stutter)
  - [Should I turn on 1080i 50p deinterlacing?](#deinterlace)
  - [How does the immersive channel preview work on Apple TV?](#tv-preview)
- **✨ AI Assistant**
  - [How do I enable, configure and switch off the AI assistant?](#agent-setup)
  - [Are there free models for the AI assistant? How do I set up NVIDIA NIM or Cloudflare?](#agent-free-model-providers)
  - [What can and can't the assistant do? Does it read my data?](#agent-scope)
  - [Does the assistant remember what I tell it? How do I manage that?](#agent-memory)
- **☁️ Pro, Sync & Support**
  - [What is the difference between Pro and free, and how do I buy it?](#pro-version)
  - [What does iCloud sync cover?](#icloud-sync)
  - [How do I contact the developer or report a problem?](#contact)

---

## 📥 Subscriptions & Setup

<a id="add-subscription"></a>

### How do I add a subscription?

nanoTV supports four kinds of subscription: M3U playlists, Xtream Codes, Stalker Portal (MAG) and TVHeadend.

- macOS: the "+" at the top right of the Subscriptions page in the sidebar, or press ⇧⌘N.
- iOS: the add button on the home screen.

The address is required. The subscription name can be left blank — nanoTV then uses the server hostname, or "New Subscription" plus the date. Xtream and Stalker also need your account details.
Once added, nanoTV downloads and parses the channel list automatically.

<a id="external-subscription-import"></a>

### How do I import a subscription from Telegram, a web page or an HTTPS link?

iPhone, iPad and Mac can import a subscription from an HTTPS link opened in Telegram, a browser, an email or a QR code.
M3U, Xtream Codes and Stalker Portal are supported.

The recommended link format is:
`https://nanotv.app/add#v=1&type=<m3u|xtream|stalker>&url=<encoded subscription address>&…`

`v`, `type` and `url` are the basics. Xtream can carry a username and password, Stalker needs a MAC address,
and you can add a subscription name, EPG address, User-Agent or Referer as needed. Percent-encode every
parameter value individually, and keep the parameters after the `#` — they must not be moved behind a `?`.
Full format and examples:

```text
https://nanotv.app/nanotv-web-open.html#part-import
```

When someone opens the link, nanoTV only shows a summary of the subscription first. Nothing is saved until
they tap "Confirm and import" themselves — the link alone never adds anything silently.

<a id="subscription-refresh"></a>

### How does automatic refresh work?

Every subscription has its own refresh interval — anything from 1 hour to 5 days — or it can refresh each time you open the app.
You set this on the subscription's edit screen. To refresh by hand: press ⇧⌘R on macOS, or use the refresh button on the subscription card.
A refresh only updates the channel list. Your favorites and tags are left untouched.

<a id="quick-play"></a>

### Can I play a single address without creating a subscription?

Yes — that is what Quick Play is for:

- macOS: Quick Play in the sidebar, or press ⌘N;
- iOS: Quick Play in the "…" menu at the top left of the home screen.

Paste a stream address and it plays. You can set a User-Agent and Referer for that one address.
Local files and WebDAV work too. Quick Play keeps its own history, separate from Recently Played,
and any entry in that history can be saved as a subscription in one tap.
You can also hand an address to the assistant and let it play the stream and manage these entries
(local files and WebDAV excepted).
To add **several** bare links at once, choose "Text import" when adding a subscription and paste one address per line.

<a id="external-playback"></a>

### Can another app, a web page or Finder hand a video to nanoTV?

Yes, three ways (iOS and macOS both support the first two; the third is macOS only):

1. An HTTPS link — best for sharing:

```text
https://nanotv.app/play?url=<percent-encoded-media-address>&title=<optional>&user-agent=<optional>&referer=<optional>
```

   It is an ordinary web address, so Telegram, WeChat, X, email and QR codes will not strip or rewrite it.
   Opening it hands the media straight to nanoTV.

2. A custom scheme — best for local automation:

```text
nanotv://play?url=<percent-encoded-media-address>&title=<optional>&user-agent=<optional>&referer=<optional>
```

   No web page in between; it launches the app on the device directly, which suits buttons on your own site,
   scripts and Shortcuts. Most chat apps filter this kind of link, so do not use it for sharing.

3. Finder on macOS: right-click a media file → Open With → nanoTV.
   To make double-click work, use Get Info → Open with → Change All to make nanoTV the default for that extension.
   mp4, mkv, mov, ts, m2ts, avi, mpeg, mpg and webm are currently supported.

Two things to watch: percent-encode each parameter value on its own (use encodeURIComponent in a web page)
rather than hand-assembling unencoded `&` or `%`; and spell the parameter names out in full — `url`, `title`,
`user-agent`, `referer`. Short forms such as `ua` or `ref` are ignored.

---

## 📺 Channels & Organizing

<a id="app-search"></a><a id="search-tips"></a>

### How do I find a channel or program quickly?

Use global search: one query covers channels and guide data across every subscription, so you do not have to open them one by one. Press ⇧⌘F on macOS.

- Search is fuzzy by default — part of a name is enough;
- for an exact match, wrap the term in straight double quotes, e.g. "CCTV5". This helps a lot when a short name matches too many channels;
- tapping the search field shows your recent searches, so you can repeat one in a tap;
- results use an adaptive grid, and you can choose how many cards fit per row.

<a id="favorites"></a>

### How do favorites work?

Tap the bookmark icon on a channel. Favorites are a single list that spans all your subscriptions.
When you start playback from the Favorites page, the player's channel panel and the next/previous controls follow the favorites list rather than the channel's own subscription.
With iCloud sync on, favorites follow you across your iOS, tvOS and macOS devices.

<a id="channel-tags"></a>

### What are channel tags for?

Tags are your own groupings across subscriptions, kept separate from the group-title the source provides.
Use them to collect channels scattered across different subscriptions into one place — "Kids" or "Sports", for example.
A tag is bound to a stable channel identity, so it survives a subscription refresh.

---

## 📋 Program Guide

<a id="epg-setup"></a><a id="multiple-epg"></a>

### How do I set up the program guide (EPG)?

The guide has two sources, tried in order:

1. the EPG address that came with the subscription (url-tvg in an M3U, supplied automatically by Xtream), or one you typed on the subscription's edit screen;
2. the global EPG address configured under Settings → Program Guide.

EPG data is XMLTV. After downloading, it is matched to channels by tvg-id and by channel name; a channel that matches on neither gets no guide.
The refresh interval is also under Settings → Program Guide.
A single field can hold **several** EPG addresses separated by commas — use ASCII commas, with no spaces before or after:

```text
https://a.example.com/g.xml,https://b.example.com/epg.xml
```

If one source goes down the others still load. Turn on "Update EPG when refreshing subscriptions" to keep the guide in step with the channel list.

On macOS the guide grid zooms freely, so you can take in a wider time range or more channels at once.

<a id="epg-missing"></a>

### Why do some channels have no guide data?

Nearly always because the channel's tvg-id does not match any channel id in the EPG file. Worth trying:

- add a better-matching EPG address on the subscription's edit screen;
- check that the global EPG under Settings → Program Guide is switched on;
- refresh that subscription's EPG by hand (Refresh EPG is in the subscription card's right-click / long-press menu).

If the source carries no data for that channel at all, there is nothing that can fill the gap.

<a id="epg-reminders"></a>

### How do program reminders work?

> ℹ️ Requires macOS & iOS 18+

Program reminders need iOS 18 or later, or macOS. tvOS is not supported.

- Turn them on: Settings → Program Guide → Enable Program Reminders. The system asks for notification permission the first time and you have to tap Allow; if you declined earlier, follow the on-screen hint to re-enable it in system notification settings.
- Add one: open the guide in the main window, then long-press (iOS) or right-click (macOS) a cell for a program that has not started yet and choose Add Reminder.
- Get notified: reminders fire 5 minutes before air time by default, and the lead time is on the same settings page. Tap the notification and nanoTV opens and starts that channel.
- Cancel: remove reminders under Settings → Program Guide → Manage Program Reminders, or choose Remove Reminder from the cell's menu.

You can also ask the assistant to look up a program and then add, list or cancel reminders — but the master switch and the system notification permission are still yours to grant.

---

## 💬 Subtitles & Translation

<a id="transcription"></a><a id="real-time-subtitles"></a>

### How do I turn on live transcription (AI subtitles)?

Choose a language model first under Settings → Subtitles / Transcription (English, Mandarin, Japanese).
The English model is built in; the Mandarin and Japanese models download once and work offline afterwards.
When the model is ready, tap Live Subtitles at the bottom of the playback screen (⌃T on macOS).
Transcription runs on your device — no audio is uploaded.

Opening the playback controls differs by platform: swipe down on tvOS, tap the menu button on iOS and macOS.

<a id="translation"></a><a id="subtitle-translation"></a>

### How do I turn on subtitle translation?

Pick a translation service under Settings → Translation Services; it reads "Service available" once verification passes. Your options:
Google, Microsoft, DeepL, any OpenAI-compatible large language model, a custom service you host yourself,
and Apple's on-device translation (macOS and iOS/iPadOS only — not tvOS).
A one-time disclaimer appears the first time; you have to accept it before you can configure anything.
During playback, tap Subtitles at the bottom to set the source and target language.
For DeepL and LLM settings see "How do I set up DeepL or LLM translation?"; for your own service see "How do I connect my own translation API?".
The two paths are independent: AI live subtitles translate the transcription, while subtitle tracks translate the subtitles carried by the stream.
The source language has to match what is actually spoken, or the output will be gibberish.

<a id="translation-deepl-llm"></a><a id="deepl-llm"></a>

### How do I set up DeepL or LLM translation?

Both live under Settings → Translation Services. Fill in the fields, tap Verify, and wait for "Service available".

- DeepL: your own API key and endpoint (the free and Pro endpoints differ — use the one that matches your key).
- LLM: endpoint, API key and model name. Anything that speaks the OpenAI API will do.

The key is yours; nanoTV neither supplies nor shares one. Credentials live in the device keychain and are not synced through iCloud.
Which to choose: an LLM reads more naturally on conversational material, but it is a remote call, so latency depends on your network and the model.
DeepL strikes a balance between quality and speed. For the lowest latency use Apple's on-device translation (macOS / iOS),
or run your own service on the local network.
Note: this sets the model used for **translation**. The assistant has its own separate model setting, and the two do not affect each other.

<a id="translation-custom-api"></a><a id="custom-translation"></a>

### How do I connect my own translation API?

nanoTV works with self-hosted translation services that speak the Google Translate API format — MTranServer, for example.
Running one on your local network gives the lowest latency.

1. Start the service with Docker: image xxnuo/mtranserver:latest, publish port 8989, mount a models directory;
   set the CORE_API_TOKEN environment variable if you want authentication.
2. Go to Settings → Translation Services → Custom API and fill in three fields (assuming the server is 192.168.1.100):
   - Base URL: http://192.168.1.100:8989
   - Path URL: /google/language/translate/v2
   - Auth token: the same value as CORE_API_TOKEN, or blank if you did not set one.

3. Tap Verify. Once it passes, the target language appears in the subtitle menu during playback.

Verification usually fails because the IP or port is wrong, the container never started, or the device and the server are on different networks.

MTranServer's deployment notes and image live at https://github.com/xxnuo/MTranServer

<a id="free-translation"></a>

### Is there a free public translation service I can use without hosting one?

There is. Thanks to Linxudo Jacopo for running a free community translation service — nothing to deploy yourself.
To use it, go to Settings → Translation Services → Custom API and fill in:

- Base URL: `https://translate.houlang.cloud`
- Path URL: leave the default unchanged
- Auth token: leave blank

Tap Verify; "Service available" means you are set.
Source: https://linux.do/t/topic/1616910 . This is a third-party community service and its availability can change at any time — for something dependable, host your own as described in "How do I connect my own translation API?".

---

## 🎞 Playback & Picture

<a id="playback-failed"></a>

### A channel will not play — what now?

In order of likelihood:

1. the source is down or the channel has been retired — try another channel in the same subscription first;
2. the source requires a particular User-Agent or Referer — set it on the subscription's edit screen;
3. the subscription has expired (an Xtream or Stalker account past its date) — check the expiry shown on the subscription card;
4. the network is restricted — Settings → Network can configure a proxy or turn on network optimization.

When playback fails the player says so in place rather than quitting, so you can switch channels and try again straight away.

<a id="live-stutter"></a><a id="live-buffer"></a>

### Live streams keep stuttering — what can I tune?

Start with the buffer: Settings → Playback lets you set the live buffer length. A longer buffer absorbs more network jitter and stutters less;
a shorter one stays closer to live. Pick the balance that suits your connection.
Also worth trying:

- HLS channels slow to start: turn on "Fast start for HLS streams";
- a source that is slow or unreachable on your current network: set a SOCKS5 or HTTP proxy under Settings → Network, or turn on network optimization;
- some sources only behave with a particular User-Agent: set one per subscription on its edit screen;
- juddering on 1080i sources such as sports and news: turn on "1080i 50p deinterlacing";
- audio out of sync on one source: update to the latest version first — mismatched audio/video PTS on unusual sources has been fixed.

If a channel **will not play at all** (black screen, an error) rather than stuttering, see "A channel will not play — what now?".

<a id="deinterlace"></a>

### Should I turn on 1080i 50p deinterlacing?

Many live channels — European sports and news in particular — are broadcast as 1080i at 25fps, which really carries 50 fields per second.
With deinterlacing on, nanoTV uses YADIF 2x to reconstruct full frames at 50p: motion is visibly smoother and the comb artifacts disappear.
Turn it on under Settings → Playback → 1080i 50p deinterlacing.
Worth having on for live sports and news. It costs some extra processing, so switch it off if it causes stutter on an older device.
Progressive sources (1080p, 4K) are unaffected.

<a id="tv-preview"></a>

### How does the immersive channel preview work on Apple TV?

On Apple TV, nanoTV plays a live preview of whichever channel you are pointing at — in the home screen hero area and in the TV Guide.
You can keep watching while you look for something else, without actually switching channels.
Previews are muted by default so browsing stays quiet; swipe up into full-screen playback and the sound comes back automatically.
The switches are under Settings → Playback, and you can control three things separately:

- home screen channel preview
- TV Guide channel preview
- preview sound

A preview opens a real stream connection. If your provider caps concurrent connections, or bandwidth is tight, turning previews off reduces the load.

---

## ✨ AI Assistant

<a id="agent-setup"></a>

### How do I enable, configure and switch off the AI assistant?

The assistant is off by default. Enabling it takes two steps, in this order — enable the assistant first, then configure the model, because the whole model section stays greyed out until the switch is on:

- iOS: Settings → Experimental Features → AI Assistant;
- macOS: Settings (⌘,) → the Assistant tab at the top.

1. Turn on "Enable AI Assistant". A short explanation appears the first time; it is only really on once you tap "Agree and enable".
2. Configure a model: pick a provider — OpenAI, xAI, DeepSeek, Kimi (China or international), Google Gemini,
   NVIDIA NIM, Cloudflare Workers AI. For anything else choose Custom API and enter any OpenAI-compatible endpoint.
   Then add your API key; the model name can be typed by hand or picked after tapping "Fetch model list".
   For free options and how to sign up with NVIDIA or Cloudflare, see "Are there free models for the AI assistant?".
3. Tap "Test connection". **The assistant does not work until this passes** — it is the step people miss most often.
   Changing the provider, Account ID, endpoint, key or model name revokes the "Verified" state, so test again.

The API key is one you obtain from the provider yourself; nanoTV neither supplies it nor pays for it. It is stored in the device keychain
and is not synced through iCloud. If you already configured a key for the same provider under subtitle translation, the assistant borrows
that one to start with (the screen says so); entering a key here switches it to the assistant's own, and the two are independent from then on.
Where to open the assistant once it is set up: on iOS the sparkle (✦) button at the top right of the home screen; on macOS click AI Assistant
in the sidebar, which opens its own window.
To switch it off, turn "Enable AI Assistant" back off and it stops immediately. Your configuration and key are kept, so re-enabling needs no
retyping and shows no second explanation — only "Reset to defaults" clears the switch, the agreement, the verified state and the key together.

<a id="agent-free-model-providers"></a>

### Are there free models for the AI assistant? How do I set up NVIDIA NIM or Cloudflare?

There are. NVIDIA NIM and Cloudflare Workers AI are both worth trying first — each has a free entry point and a choice of models.
Quotas, available models and limits are whatever the provider's own page currently says.

- NVIDIA NIM: sign up or sign in at https://build.nvidia.com , open a model page and click "Get API Key", then copy the key
  (it usually starts with nvapi-). Back in Settings → AI Assistant, choose NVIDIA NIM as the provider, paste the key, and either keep
  the default model `nvidia/nemotron-3-super-120b-a12b` or fetch the model list and pick another. NVIDIA's hosted API includes a free
  allowance for prototyping; your account page is the authority on what is left.
- Cloudflare Workers AI: sign up or sign in, then open
  https://dash.cloudflare.com/?to=/:account/ai/workers-ai , click "Use REST API", copy the Account ID and create a Workers AI API token.
  Back in the assistant settings, choose Cloudflare Workers AI and fill in both values; the default model `@cf/nvidia/nemotron-3-120b-a12b`
  is a fine starting point. The free plan includes 10,000 Neurons per day, reset at 00:00 UTC; a few models require a paid plan.

Always finish by tapping "Test connection" — the assistant is unavailable until it passes. What you configure here is the assistant's own
model, independent of the DeepL / LLM settings used for subtitle translation. Never share an API key or token.

<a id="agent-scope"></a>

### What can and can't the assistant do? Does it read my data?

It can: list subscriptions, search channels, look up the guide, start and stop playback; add, edit, refresh and delete subscriptions;
manage favorites, recently played and channel tags; play a stream address you give it and manage those Quick Play entries
(including saving them as subscriptions); and answer questions about using nanoTV.
For four actions — deleting a subscription, deleting a tag, clearing Quick Play history and refreshing every subscription — it asks first and waits for your answer.
Adding a subscription is subject to the free-tier limit like everything else: at the limit the assistant cannot add one either. That restriction is in the code.
It cannot: reach anything outside nanoTV. It does not search the web, read your files or change system settings;
it also leaves local-file and WebDAV Quick Play alone, since those need you to grant access in the panel yourself.
This boundary is enforced in code: the assistant can only call registered tools, and anything outside that registry is refused.

Where your data goes — the question people ask most, answered plainly rather than reassuringly:

- The assistant **does not** read other files on your device, **does not** browse the web on its own, and does not change system settings.
  Everything it reads is nanoTV's own data: subscriptions, channels, guide data, favorites, tags and playback state.
- But it is a large language model at heart. Your questions, plus whatever nanoTV data is needed to answer them (channel names,
  subscription names and the like), are sent to **the provider you configured yourself** in settings.
  So do not type anything private into the conversation. Which provider, and whether anything is sent at all, follows your configuration and the master switch.
- These never enter the model's context: API keys (kept in the device keychain, and not synced through iCloud),
  subscription passwords, and the full addresses in Quick Play history (which often carry an account or auth token).
- What the assistant remembers (see "Does the assistant remember what I tell it?") is **persistent**: it is sent along with every
  question from then on, not just once. That is why addresses and credentials cannot go into memory either — the code blocks it, rather than trusting the assistant to behave.
- It does not upload your media either: transcription runs on the device and no audio leaves it.

<a id="agent-memory"></a>

### Does the assistant remember what I tell it? How do I manage that?

It does, but only the kind of thing you ask it to remember, and it is stored **on this device only** — not in iCloud, and not across devices.

How to make it remember: just say so — "remember that when I say play badminton, play Hub Sports from Gary Club",
or "remember to keep your answers short". A long-term note like that comes along automatically in every later conversation, so you never repeat it.
The assistant also notes a preference on its own when you mention it repeatedly; it tells you at the time what it wrote down,
and that kind **expires after ninety days** unless you explicitly say "remember" to make it permanent.
If you would rather it never did that, turn off "Allow the assistant to remember on its own" under Settings → Features → AI Assistant;
the notes you asked for out loud are unaffected.

How to manage it: the "⋯" menu in the assistant window → Memory shows everything it holds, who wrote each note and when it expires.
You can delete them one at a time or clear the lot. Saying "forget that" in the conversation works too.
It holds ten notes at most — when full, the assistant reads out what it already has and asks which one to replace rather than dropping one itself.

Two things you have to know:

- Memory is sent to your configured model provider with every question. Do not put anything private in it.
- Addresses, accounts, passwords and tokens **cannot** be written to it: the code blocks that, so the assistant could not store them if it tried.
  To check a subscription password, open the Edit Subscription panel.

---

## ☁️ Pro, Sync & Support

<a id="pro-version"></a>

### What is the difference between Pro and free, and how do I buy it?

Pro and free differ in exactly three ways; everything else is identical in both:

- Subscriptions: free allows 1 subscription, Pro is unlimited;
- iCloud sync: only Pro syncs subscriptions and settings — free does not sync;
- AI subtitles (live transcription): free runs up to 3 minutes at a time, Pro has no time limit.

Buying it, and how long it lasts:

- A one-time in-app purchase, **not a subscription**. Once bought it is permanent for the current product and never expires.
- You buy it under Settings → Pro. Payment and refunds are handled by the App Store.
- US$7.99 on the US App Store; other countries and regions are converted at the exchange rate, and the App Store price is the one that counts.
- With no balance and no payment method on your App Store account, you can top up with an Apple gift card first, then buy.

Buying Pro is the strongest vote of confidence you can give the developer, and it is much appreciated.

One purchase covers all three platforms: iOS, macOS and tvOS, as long as you are signed in with the **same Apple Account**.
On another device, go to Settings → Pro and tap "Restore Purchase".
If that device has the TestFlight build installed, delete it first, download the App Store version, and then restore.

<a id="icloud-sync"></a>

### What does iCloud sync cover?

Turn it on under Settings → iCloud. It syncs subscriptions, favorites and your common settings.
Every device has to be signed in to the same Apple Account; on tvOS the default user must be that same account.
Credentials such as API keys stay in each device's own keychain and are **not** synced.

<a id="contact"></a>

### How do I contact the developer or report a problem?

Three channels. For problem reports **Telegram is best** — new builds are announced there and the developer replies there:

- Telegram: https://t.me/nanotvinfo
- Website: https://nanotv.app
- Email: nanotv.apps@gmail.com

When reporting a playback problem, please include the subscription type (M3U / Xtream / Stalker), the channel name and what
exactly you saw. The version and build number help too, and they make the cause much faster to pin down.

The assistant cannot send an email or a message on your behalf — it can only give you the address for you to use yourself.

---

Still stuck? Visit [nanotv.app](https://nanotv.app) or join the [Telegram Community](https://t.me/nanotvinfo).
