# 🤖 ChatGPT Telegram 智慧助理機器人

[![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![OpenAI SDK](https://img.shields.io/badge/OpenAI_SDK->=1.40.0-orange.svg?logo=openai&logoColor=white)](https://platform.openai.com/)
[![PTB Version](https://img.shields.io/badge/python--telegram--bot->=20.7-2CA5E0.svg?logo=telegram&logoColor=white)](https://python-telegram-bot.org/)
[![License](https://img.shields.io/badge/License-GPL%202.0-brightgreen.svg)](LICENSE)
[![Docker Ready](https://img.shields.io/badge/Docker-Ready-2496ED.svg?logo=docker&logoColor=white)](Dockerfile)

這是一個功能強大且高度可自訂的 [Telegram 機器人](https://core.telegram.org/bots/api)，整合了 OpenAI 最新世代的模型（包含 **GPT-6 Astra**、**GPT-5 系列**、**o-series 深度推理模型**、**GPT-4o**、**GPT-Image-1**、**DALL·E 3**、**Whisper** 及 **TTS** 語音合成 API），並具備 16 款多功能 Function Calling 擴充外掛。

只需極簡設定，即可在私聊與群組中擁有頂級 AI 智慧助理！

---

## ✨ 核心功能特色

- 🧠 **支援最新世代 AI 模型**
  - 支援 **50+ 款** OpenAI 最新模型：GPT-6 Astra、GPT-5.6 (Sol / Terra / Luna / Cyber)、GPT-5.5、GPT-5.4、GPT-5、o1 / o3 / o4 系列深度推理模型、GPT-4o 與 GPT-4o-mini 等。
- ⚡ **打字流式傳輸（Streaming）**
  - 即時逐字輸出回覆，宛如真人即時打字互動，大幅降低等待感。
- 👁️ **強大多模態視覺理解（Vision）**
  - 支援直接傳送照片與文件圖片進行影像辨識、內容解讀與連續多輪對話追問（預設搭載 `gpt-4o`）。
- 🎨 **最新 AI 圖像生成**
  - 透過 `/image` 指令使用 `gpt-image-1` 或 `dall-e-3` 產生高畫質圖像，支援多種風格與尺寸自訂。
- 🎙️ **語音轉文字與文字轉語音（Audio & TTS）**
  - 支援語音/影片訊息自動轉錄（基於 Whisper API）。
  - 支援使用 `/tts` 指令或語音外掛進行自然擬真的語音合成朗讀。
- 🔌 **16 種 Function Calling 外掛系統**
  - 支援網路搜尋（DuckDuckGo）、多國語言翻譯（DeepL / DuckDuckGo）、天氣預報、WolframAlpha 專業運算、Spotify 控制、加密貨幣即時行情、網頁截圖等功能。
- 💰 **預算控管與 Token 統計系統**
  - 提供 `/stats` 指令查詢今日、當月與對話總 Token 用量及花費。
  - 可為不同使用者設定專屬預算上限（日/月/總量），並支援群組訪客預算控管。
- 🛡️ **權限與存取控制**
  - 支援白名單機制（`ALLOWED_TELEGRAM_USER_IDS`）與管理員專屬身分（`ADMIN_USER_IDS`）。
- 📝 **智慧長對話記憶與自動摘要**
  - 超出歷史上限或模型 Context 視窗時，自動產生記憶摘要，兼顧對話連續性並避免過度消耗 Token。
- 🌐 **支援第三方自訂 API 端點 (`OPENAI_BASE_URL`)**
  - 可輕鬆對接 Ollama、vLLM、DeepSeek、LocalAI 或其他相容 OpenAI 協定的本地/自建大模型服務。
- 🌍 **完整繁體中文與多國語系**
  - 內建包含繁體中文 (`zh-tw`)、簡體中文 (`zh-cn`)、英文 (`en`) 等 18+ 種介面語言。
- 🐳 **完整容器化支援**
  - 提供現代化 Dockerfile (Python 3.11-slim) 與 Docker Compose 設定檔，開箱即用。

---

## 📋 支援模型一覽

本專案採用動態設定架構，支援 OpenAI 所有主流與最新模型：

| 模型系列 | 代表型號名稱（`OPENAI_MODEL`） | 上下文長度 (Context) | 說明與適用場景 |
| :--- | :--- | :--- | :--- |
| **GPT-6 系列** | `gpt-6-astra` | 200k | 最新世代旗艦級語言模型，極致推理與表達能力 |
| **GPT-5.6 系列** | `gpt-5.6-sol`, `gpt-5.6-terra`, `gpt-5.6-luna`, `gpt-5.6-cyber` | 200k | 高階專門領域與全方位推論模型 |
| **GPT-5.x 系列** | `gpt-5.5`, `gpt-5.5-pro`, `gpt-5.4`, `gpt-5.4-mini`, `gpt-5` | 200k | GPT-5 系列高性價比與主力模型 |
| **o-series 系列** | `o1`, `o1-mini`, `o3`, `o3-mini`, `o3-pro`, `o4-mini` | 128k ~ 200k | 具備強化自我思考（CoT）之高難度邏輯/數學/程式推理模型 |
| **GPT-4o 系列** | `gpt-4o-mini`（預設）、`gpt-4o` | 128k | 兼具極速反應、視覺支援與極低成本的通用首選 |
| **視覺模型** | `gpt-4o`（預設 `VISION_MODEL`） | 128k | 頂尖多模態圖片識別與圖文交談 |
| **影像生成** | `gpt-image-1`（預設 `IMAGE_MODEL`）、`dall-e-3` | - | 支援高品質圖片生成與風格調整 |
| **語音服務** | `whisper-1`（轉錄）、`tts-1` / `tts-1-hd`（合成） | - | 語音轉文字與文字朗讀 |

---

## 🚀 快速上手指南

### 1. 前置準備
1. **Python 環境**：Python 3.10 以上版本。
2. **Telegram 機器人 Token**：
   - 在 Telegram 搜尋 [@BotFather](https://t.me/botfather) 並發送 `/newbot` 依提示建立機器人，取得 `TELEGRAM_BOT_TOKEN`。
3. **OpenAI API Key**：
   - 前往 [OpenAI API Keys](https://platform.openai.com/api-keys) 申請 API 金鑰。
4. **查詢您的 Telegram User ID**：
   - 在 Telegram 搜尋 [@userinfobot](https://t.me/userinfobot) 或 [@getidsbot](https://t.me/getidsbot) 取得您的數字 ID。

---

### 2. 本機部署 (Local Setup)

```bash
# 1. 複製專案庫
git clone https://github.com/SAOJSM/chatgpt-telegram-bot.git
cd chatgpt-telegram-bot

# 2. 建立並啟動 Python 虛擬環境
python -m venv venv

# Windows 啟用方式：
venv\Scripts\activate

# Linux / macOS 啟用方式：
source venv/bin/activate

# 3. 安裝相依套件
pip install -r requirements.txt

# 4. 配置環境變數
cp .env.example .env
# 請使用文字編輯器（如 VS Code、Notepad）開啟 .env 填寫必要參數

# 5. 啟動機器人
python bot/main.py
```

> [!TIP]
> 如果您打算使用語音訊息轉錄功能，本機系統需預先安裝 [ffmpeg](https://ffmpeg.org/)（Windows 可使用 `winget install Gyan.FFmpeg` 或 `choco install ffmpeg`）。

---

### 3. 使用 Docker 部署 (Docker & Docker Compose)

專案已內建最佳化 Dockerfile（基於 `python:3.11-slim` 並內建 `ffmpeg`）。

#### 使用 Docker Compose（推薦）：
```bash
# 複製並編輯環境變數
cp .env.example .env
nano .env

# 背景啟動容器
docker compose up -d

# 檢視運行日誌
docker compose logs -f
```

#### 手動建置並執行 Docker：
```bash
docker build -t chatgpt-telegram-bot .
docker run -d --name chatgpt-bot --env-file .env --restart unless-stopped chatgpt-telegram-bot
```

---

## ⚙️ 環境設定說明 (`.env`)

複製 `.env.example` 為 `.env`，主要設定項目如下：

### 🔑 核心必填項目
| 參數名稱 | 說明 | 範例 / 預設值 |
| :--- | :--- | :--- |
| `OPENAI_API_KEY` | OpenAI API 金鑰 | `sk-...` |
| `TELEGRAM_BOT_TOKEN` | Telegram Bot API 權杖 | `123456789:ABCdef...` |
| `ALLOWED_TELEGRAM_USER_IDS` | 允許使用機器人的 Telegram User ID（以逗號分隔）；填 `*` 代表所有人皆可使用 | `*` 或 `123456789,987654321` |
| `ADMIN_USER_IDS` | 管理員 Telegram User ID，具備管理指令且無預算限制；`-` 代表不設管理員 | `-` 或 `123456789` |

### 🧠 模型與對話設定
| 參數名稱 | 說明 | 預設值 |
| :--- | :--- | :--- |
| `OPENAI_MODEL` | 預設對話模型 | `gpt-4o-mini` |
| `OPENAI_BASE_URL` | 自訂 API 端點（適用於 Ollama, vLLM, DeepSeek, LocalAI） | 留空（預設官方端點） |
| `ASSISTANT_PROMPT` | 系統提示詞（System Prompt） | `You are a helpful assistant.` |
| `STREAM` | 是否啟用逐字流式傳輸 | `true` |
| `SHOW_USAGE` | 每次回覆後是否顯示 Token 消耗與花費統計 | `false` |
| `MAX_TOKENS` | 機器人單次回答最大 Token 數量 | 動態匹配模型上限 |
| `MAX_HISTORY_SIZE` | 記憶對話上限則數，超過將自動摘要壓縮 | `15` |
| `MAX_CONVERSATION_AGE_MINUTES` | 對話閒置多久自動重設記憶（分鐘） | `180` |
| `BOT_LANGUAGE` | 機器人系統提示語系（如 `zh-tw`, `zh-cn`, `en` 等） | `en` |

### 🖼️ 視覺與影像生成
| 參數名稱 | 說明 | 預設值 |
| :--- | :--- | :--- |
| `ENABLE_VISION` | 是否啟用圖片視覺分析 | `true` |
| `VISION_MODEL` | 視覺分析模型 | `gpt-4o` |
| `VISION_PROMPT` | 預設解讀圖片時的提示詞 | `What is in this image` |
| `ENABLE_IMAGE_GENERATION` | 是否啟用 `/image` 生圖指令 | `true` |
| `IMAGE_MODEL` | 圖像生成模型（如 `gpt-image-1`, `dall-e-3`, `dall-e-2`） | `gpt-image-1` |
| `IMAGE_SIZE` | 生成圖片尺寸（如 `1024x1024`, `512x512`） | `512x512` |
| `IMAGE_QUALITY` | 圖片品質（適用於 DALL·E 3：`standard` 或 `hd`） | `standard` |
| `IMAGE_STYLE` | 圖片風格（適用於 DALL·E 3：`vivid` 或 `natural`） | `vivid` |

### 🎙️ 語音與文字朗讀 (TTS & Whisper)
| 參數名稱 | 說明 | 預設值 |
| :--- | :--- | :--- |
| `ENABLE_TRANSCRIPTION` | 是否開啟語音/影片訊息語音轉文字 | `true` |
| `ENABLE_TTS_GENERATION` | 是否啟用 `/tts` 語音朗讀指令 | `true` |
| `TTS_MODEL` | 語音合成模型（`tts-1` 或 `tts-1-hd`） | `tts-1` |
| `TTS_VOICE` | 朗讀聲音（`alloy`, `echo`, `fable`, `onyx`, `nova`, `shimmer`） | `alloy` |

### 💵 預算與配額控制
| 參數名稱 | 說明 | 預設值 |
| :--- | :--- | :--- |
| `BUDGET_PERIOD` | 預算重設週期：`daily`（每日）、`monthly`（每月）、`all-time`（不重設） | `monthly` |
| `USER_BUDGETS` | 依序設定白名單使用者的預算金額（美元），`*` 代表不限 | `*` |
| `GUEST_BUDGET` | 群組中非白名單訪客的共用額度（美元） | `100.0` |

### 🌐 網路代理設定 (Proxy)
| 參數名稱 | 說明 | 範例 |
| :--- | :--- | :--- |
| `PROXY` | 同時設定 Telegram 與 OpenAI 的連線代理 | `http://127.0.0.1:7890` |
| `OPENAI_PROXY` | 僅針對 OpenAI API 使用的代理 | `http://127.0.0.1:7890` |
| `TELEGRAM_PROXY` | 僅針對 Telegram Bot 連線使用的代理 | `http://127.0.0.1:7890` |

---

## 🔌 擴充外掛功能 (Plugins)

本專案支援 OpenAI Function Calling 外掛機制。欲啟用外掛，請在 `.env` 中設定 `ENABLE_FUNCTIONS=true` 並指定 `PLUGINS`：

```env
ENABLE_FUNCTIONS=true
PLUGINS=ddg_web_search,weather,crypto,wolfram
SHOW_PLUGINS_USED=true
```

| 外掛名稱 | 功能說明 | 必要環境變數 | 相依套件 |
| :--- | :--- | :--- | :--- |
| `ddg_web_search` | DuckDuckGo 即時網路搜尋 | 無 | `duckduckgo_search` |
| `ddg_image_search`| DuckDuckGo 圖片/GIF 搜尋 | 無 | `duckduckgo_search` |
| `ddg_translate` | DuckDuckGo 快速語言翻譯 | 無 | `duckduckgo_search` |
| `deepl_translate`| DeepL 高品質多語言翻譯 | `DEEPL_API_KEY` | - |
| `weather` | 即時天氣與 7 天天氣預報 (Open-Meteo) | 無 | - |
| `crypto` | 加密貨幣即時行情報價 (CoinCap) | 無 | - |
| `wolfram` | WolframAlpha 知識運算引擎 | `WOLFRAM_APP_ID` | `wolframalpha` |
| `spotify` | Spotify 熱門歌曲搜尋與播放控制 | `SPOTIFY_CLIENT_ID`, `SPOTIFY_CLIENT_SECRET`, `SPOTIFY_REDIRECT_URI` | `spotipy` |
| `worldtimeapi` | 查詢全球各時區即時標準時間 | `WORLDTIME_DEFAULT_TIMEZONE` | - |
| `webshot` | 網站首頁即時截圖產生 | 無 | - |
| `whois` | 網域名稱 Whois 資訊查詢 | 無 | `whois` |
| `youtube_audio_extractor` | 提取 YouTube 影片中的音訊檔案 | 無 | `pytube` |
| `gtts_text_to_speech` | Google TTS 語音朗讀 | 無 | `gtts` |
| `auto_tts` | 自動 OpenAI TTS 語音回覆 | 無 | - |
| `dice` | 在聊天室中擲骰子趣味功能 | 無 | - |

---

## 💬 機器人指令說明

在 Telegram 聊天室中可使用以下斜線指令：

- `/help` - 顯示機器人說明與所有支援指令
- `/reset` - 重設當前會話記憶，重新開啟新話題
- `/stats` - 查詢個人 Token 用量、預算餘額與今日花費統計
- `/resend` - 重新發送上一次的使用者提問
- `/image <提示詞>` - 根據描述使用 AI 生成精美圖片
- `/tts <文字>` - 將輸入的文字轉換成語音朗讀檔案
- `/chat <訊息>` - 在群組對話中主動呼叫機器人回覆（需加入群組）

> [!NOTE]
> 若要啟用**內聯查詢（Inline Mode）**，可在 Telegram 向 [@BotFather](https://t.me/botfather) 發送 `/setinline` 指令為您的機器人開啟 Inline 功能，即可在任何聊天視窗中輸入 `@您的機器人名稱 <問題>` 即時取得解答！

---

## ❓ 常見問題 (FAQ)

<details>
<summary><b>Q1: 機器人無法讀取語音訊息或拋出 ffmpeg 錯誤？</b></summary>

Whisper 轉錄音訊需使用 `ffmpeg` 進行音訊編解碼轉換。
- **本機環境**：請確認系統已安裝 `ffmpeg` 並將其路徑加入環境變數 `PATH`。
- **Docker 環境**：內建 Dockerfile 已預先安裝 `ffmpeg`，無需額外手動配置。
</details>

<details>
<summary><b>Q2: 如何在 Telegram 群組中使用機器人？</b></summary>

1. 將機器人加入群組。
2. 在群組中使用 `/chat <問題>` 或直接回覆機器人的訊息進行對話。
3. 若希望機器人在群組中收到每則訊息都能看到，請在 [@BotFather](https://t.me/botfather) 中透過 `/setprivacy` 將 Group Privacy 設為 `Disable`。
</details>

<details>
<summary><b>Q3: 如何介接本地 Ollama 或自建大模型服務？</b></summary>

在 `.env` 設定檔中指定自訂端點與相容模型即可，例如：
```env
OPENAI_BASE_URL=http://localhost:11434/v1/
OPENAI_MODEL=llama3.1:latest
OPENAI_API_KEY=ollama
```
</details>

---

## 📜 授權協議 (License)

本專案基於 [GPL 2.0 授權條款](LICENSE) 開源釋出。

## 🤝 致謝 (Credits)

- OpenAI 團隊提供的 [OpenAI API](https://platform.openai.com/)
- [python-telegram-bot](https://python-telegram-bot.org/) 團隊提供出色的非同步 Telegram 框架
- 原始專案開源社群貢獻者們的無私付出
