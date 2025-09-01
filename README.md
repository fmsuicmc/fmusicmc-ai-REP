# fmusicmc ai — Smart Twitter/X Replies

> **by fmusicmc Gemgym team**  
> Generate short, on‑topic replies for Twitter/X using LLMs (OpenAI‑compatible) with optional web search (SerpAPI/Wikipedia).

---
<div style="text-align:center;">
  <a href="https://ibb.co/tp0xcHrv">
    <img src="https://i.ibb.co/b542L69C/photo-2025-09-02-00-32-16.jpg" alt="photo-2025-09-02-00-32-16" border="0">
  </a>
</div>


## Features
- Floating **fmusicmc ai** button on Twitter/X
- One‑click panel: analyze tweet → generate concise reply → insert into reply box (no auto‑send)
- Tone control (friendly / professional / witty / analytical / neutral)
- Entity extraction (hashtags, cashtags, mentions, keywords)
- Optional web search via **SerpAPI**; Wikipedia fallback
- Works with any **OpenAI‑compatible** API (OpenRouter, OpenAI, custom, local/Ollama)
- Clean glassmorphism UI, Shadow DOM, MV3

---

## Quick Start (EN)

1. **Download / Load Unpacked**
   - Go to `chrome://extensions/` → enable **Developer mode**
   - **Load unpacked** → select the `fmusicmc-ai` folder

2. **Configure (OpenRouter)**
   - Click **Details → Extension options** or open `options.html`
   - Set:
     - **Provider**: `openrouter` (or `custom`)
     - **API Endpoint**: `https://openrouter.ai/api/v1/chat/completions`
     - **Model**: e.g. `openai/gpt-4o-mini` (or any model you have access to on OpenRouter)
     - **API Key**: your `sk-or-...` key from OpenRouter
   - (Optional) **SerpAPI Key** if you want web search context

3. **Use on Twitter/X**
   - Open any tweet, click the floating **fmusicmc ai** button
   - Choose a tone → **Generate** → **Insert into reply box**
   - You press **Send** (auto‑send is intentionally disabled)

### Important Notes
- The extension calls an OpenAI‑style `/v1/chat/completions` endpoint.  
- For **OpenRouter**, extra headers are sent automatically:
  - `Authorization: Bearer <sk-or-...>`
  - `HTTP-Referer: https://x.com`
  - `X-Title: fmusicmc ai`
- If you see `401 invalid_api_key`, double‑check **Endpoint**, **Model**, and your **key**.
- If you previously saw `import() is disallowed on ServiceWorkerGlobalScope`, this build uses ES module imports in `background.js` and is fixed.

---

## شروع سریع (FA)

1. **نصب افزونه**
   - به `chrome://extensions/` برو و **Developer mode** را روشن کن.
   - روی **Load unpacked** بزن و پوشه‌ی `fmusicmc-ai` را انتخاب کن.

2. **تنظیمات (OpenRouter)**
   - وارد صفحه‌ی تنظیمات افزونه شو (`options.html`).
   - مقدارها را این‌طور بگذار:
     - **Provider**: `openrouter` (یا `custom`)
     - **API Endpoint**: `https://openrouter.ai/api/v1/chat/completions`
     - **Model**: مثلاً `openai/gpt-4o-mini`
     - **API Key**: کلید `sk-or-...` از OpenRouter
   - (اختیاری) **SerpAPI Key** برای فعال‌کردن جستجو

3. **استفاده در X (توییتر)**
   - توییت را باز کن، روی دکمه‌ی شناور **fmusicmc ai** بزن.
   - تون پاسخ را انتخاب کن → **تولید پاسخ** → **قرار دادن در باکس ریپلای**
   - ارسال خودکار نداریم؛ خودت دکمه‌ی **Send** را بزن.

### نکات مهم
- افزونه با APIهای سازگار با OpenAI کار می‌کند (ساختار `/v1/chat/completions`).  
- برای **OpenRouter** هدرهای لازم به‌صورت خودکار اضافه می‌شود:
  - `Authorization: Bearer <sk-or-...>`
  - `HTTP-Referer: https://x.com`
  - `X-Title: fmusicmc ai`
- خطای `401 invalid_api_key` معمولاً از اشتباه بودن Endpoint/Model/Key است.
- خطای `import() is disallowed …` در این نسخه رفع شده است (استفاده از ES Modules).

---

## File Structure
```
fmusicmc-ai/
├─ manifest.json
├─ background.js              # MV3 service worker (ES module)
├─ content.js                 # injects UI panel + FAB button
├─ lib/
│  ├─ utils.js                # language/keywords/helpers
│  ├─ search.js               # SerpAPI + Wikipedia fallback
│  └─ llm.js                  # OpenAI-style chat API client (OpenRouter headers)
├─ options.html / options.js  # settings page
├─ popup.html / popup.js      # quick actions
├─ styles/overlay.css         # glass UI
├─ assets/
│  ├─ logo_main.png           # main project logo (portrait)
│  └─ logo_gemgym.png         # Gemgym co‑branding
└─ icons/                     # Chrome icons (derived from portrait)
```

---

## Configuration Details

### OpenRouter
- **Endpoint**: `https://openrouter.ai/api/v1/chat/completions`
- **Model**: any model string OpenRouter supports (e.g. `openai/gpt-4o-mini`, `anthropic/claude-3.5-sonnet`, …)
- **API Key**: `sk-or-...`
- Sent headers (by `lib/llm.js`):
```http
Authorization: Bearer <sk-or-...>
Content-Type: application/json
HTTP-Referer: https://x.com
X-Title: fmusicmc ai
```

### OpenAI (optional alternative)
- **Endpoint**: `https://api.openai.com/v1/chat/completions`
- **Model**: e.g. `gpt-4o-mini`
- **API Key**: your `sk-...` OpenAI key

### Local / Custom (Ollama etc.)
- **Provider**: `custom`
- **Endpoint**: e.g. `http://localhost:11434/v1/chat/completions`
- **Model**: model name exposed by your server
- **API Key**: leave empty if not required

---

## Privacy
- No analytics. Keys are stored via Chrome `storage.sync` on your device account.  
- We **do not** auto‑send tweets; you always confirm before posting.

---

## Troubleshooting
- **Nothing inserted into reply box** → X occasionally changes DOM. Try copy‑to‑clipboard, paste manually, or update extension.
- **401** → Wrong key/model/endpoint. For OpenRouter ensure the endpoint and model exist for your account.
- **429** → Rate limited by provider; slow down or switch model.
- **CORS on SerpAPI/Wikipedia** → It’s client‑side fetch; SerpAPI recommended with API key.

---

## License

```
fmusicmc ai — © fmusicmc Gemgym team. All rights reserved.
Contact: https://x.com/mr_satoshiii — @fmusicmc_P
```

Using the code implies acceptance that the **fmusicmc Gemgym team** holds full rights to the project name, branding, and included logos , . Third‑party model/API usage is subject to their respective terms.
