# ChatGPT Telegram 機器人
![python-版本](https://img.shields.io/badge/python-3.9-blue.svg)
[![openai-版本](https://img.shields.io/badge/openai-0.27.8-orange.svg)](https://openai.com/)
[![許可證](https://img.shields.io/badge/License-GPL%202.0-brightgreen.svg)](LICENSE)
[![發佈Docker 映像](https://github.com/n3d1117/chatgpt-telegram-bot/actions/workflows/publish.yaml/badge.svg)]

Telegram 機器人](https://core.telegram.org/bots/api) 與OpenAI 的_official_ [ChatGPT](https://openai.com/blog/chatgpt/)、[DALL-E](https:/ /openai.com/product/dall-e-2) 和[Whisper](https://openai.com/research/whisper) API 集成，以提供答案。 只需極少的配置即可使用。

### 螢幕截圖

#### 範例
![demo](https://user-images.githubusercontent.com/11541888/225114786-0d639854-b3e1-4214-b49a-e51ce8c40387.png)

### 擴充功能
![plugins](https://github.com/n3d1117/chatgpt-telegram-bot/assets/11541888/83d5e0cd-e09a-463d-a292-722f919e929f)

## 功能
- [x] 在答案中支援標記符
- [x] 使用`/reset`指令重設對話
- [x] 產生回覆時的打字指示器
- 可透過指定允許存取的使用者清單限制存取權限
- [x] 支援 Docker 和代理
- 透過 `/image` 指令使用 DALL-E 產生影像
- [x] 使用 Whisper 轉錄音訊和視訊資訊（可能需要 [ffmpeg](https://ffmpeg.org)
- [x] 自動會話摘要，避免過度使用令牌
- [x] 追蹤每個使用者的令牌使用情況 - 由 [@AlexHTW](https://github.com/AlexHTW) 提供
- [x] 透過"/stats "指令取得個人令牌使用統計資訊--作者：[@AlexHTW](https://github.com/AlexHTW)
- [x] 使用者預算與訪客預算 - 作者：[@AlexHTW](https://github.com/AlexHTW)
- [x] 支援流
- [x] 支持 GPT-4
   - 如果您可以存取 GPT-4 API，只需將 `OPENAI_MODEL` 參數變更為 `gpt-4
- [x] 本地化機器人語言
   - 可用語言:Brazil: :cn: :finland: :de: :indonesia: :iran: :it: :malaysia: :netherlands: :poland: :ru: :saudi_arabia: :es: :taiwan: :tr： : 烏克蘭 : :英國: :烏茲別克: :越南：
- [x] 改進了群組聊天和私聊的內嵌查詢支援 - 作者：[@bugfloyd](https://github.com/bugfloyd)
   - 若要使用此功能，請在 BotFather 中透過 `/setinline` [command](https://core.telegram.org/bots/inline) 為您的機器人啟用內聯查詢。
- [x] 支援*新機型* [2023年6月13日發表](https://openai.com/blog/function-calling-and-other-api-updates)
- [x] 支援*功能*（外掛程式），透過第三方服務擴充機器人的功能
   - 天氣、Spotify、網路搜尋、文字轉語音等。 可用插件清單請參閱[此處]（#available-plugins）。
- [x] 支援與 OpenAI 相容的非官方 API - 作者：[@kristaller486](https://github.com/kristaller486)
- [x]（新功能！）支援GPT-4 Turbo 和DALL-E 3 [2023年11月6日宣布](https://openai.com/blog/new-models-and-developer-products-announced -at-devday) - 作者：[@AlexHTW](https://github.com/AlexHTW)
- [x]（新功能！）支援文字轉語音[2023 年11 月6 日宣布](https://platform.openai.com/docs/guides/text-to-speech) - 作者：[@gilcu3] (https://github.com/gilcu3)
- [x]（新功能！）視覺支援[2023 年11 月6 日宣布](https://platform.openai.com/docs/guides/vision) - 作者：[@gilcu3](https://github .com/gilcu3)

## 附加功能 - 需要協助！
如果您想提供協助，請查看 [issues](https://github.com/n3d1117/chatgpt-telegram-bot/issues) 部分並貢獻自己的力量！
如果您想協助翻譯，請查看 [翻譯手冊](https://github.com/n3d1117/chatgpt-telegram-bot/discussions/219)

我們隨時歡迎您提交 PR！

## 前提條件
- Python 3.9 以上版本
- 一個[Telegram 機器人](https://core.telegram.org/bots#6-botfather) 及其令牌（參見[tutorial](https://core.telegram.org/bots/tutorial#obtain-your -bot-token)
- 一個 [OpenAI](https://openai.com) 帳戶（請參閱 [配置](#configuration) 部分）

### 入門

### 配置
複製 `.env.example` 並將其重新命名為 `.env`，然後根據需要編輯所需參數，從而自訂配置：

| Parameter                   | Description                                                                                                                                                                                                                   |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `OPENAI_API_KEY`            | Your OpenAI API key, you can get it from [here](https://platform.openai.com/account/api-keys)                                                                                                                                 |
| `TELEGRAM_BOT_TOKEN`        | Your Telegram bot's token, obtained using [BotFather](http://t.me/botfather) (see [tutorial](https://core.telegram.org/bots/tutorial#obtain-your-bot-token))                                                                  |
| `ADMIN_USER_IDS`            | Telegram user IDs of admins. These users have access to special admin commands, information and no budget restrictions. Admin IDs don't have to be added to `ALLOWED_TELEGRAM_USER_IDS`. **Note**: by default, no admin (`-`) |
| `ALLOWED_TELEGRAM_USER_IDS` | A comma-separated list of Telegram user IDs that are allowed to interact with the bot (use [getidsbot](https://t.me/getidsbot) to find your user ID). **Note**: by default, *everyone* is allowed (`*`)                       |

### Optional configuration
The following parameters are optional and can be set in the `.env` file:

#### Budgets
| Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                               | Default value      |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|
| `BUDGET_PERIOD`       | Determines the time frame all budgets are applied to. Available periods: `daily` *(resets budget every day)*, `monthly` *(resets budgets on the first of each month)*, `all-time` *(never resets budget)*. See the [Budget Manual](https://github.com/n3d1117/chatgpt-telegram-bot/discussions/184) for more information                                                                  | `monthly`          |
| `USER_BUDGETS`        | A comma-separated list of $-amounts per user from list `ALLOWED_TELEGRAM_USER_IDS` to set custom usage limit of OpenAI API costs for each. For `*`- user lists the first `USER_BUDGETS` value is given to every user. **Note**: by default, *no limits* for any user (`*`). See the [Budget Manual](https://github.com/n3d1117/chatgpt-telegram-bot/discussions/184) for more information | `*`                |
| `GUEST_BUDGET`        | $-amount as usage limit for all guest users. Guest users are users in group chats that are not in the `ALLOWED_TELEGRAM_USER_IDS` list. Value is ignored if no usage limits are set in user budgets (`USER_BUDGETS`=`*`). See the [Budget Manual](https://github.com/n3d1117/chatgpt-telegram-bot/discussions/184) for more information                                                   | `100.0`            |
| `TOKEN_PRICE`         | $-price per 1000 tokens used to compute cost information in usage statistics. Source: https://openai.com/pricing                                                                                                                                                                                                                                                                          | `0.002`            |
| `IMAGE_PRICES`        | A comma-separated list with 3 elements of prices for the different image sizes: `256x256`, `512x512` and `1024x1024`. Source: https://openai.com/pricing                                                                                                                                                                                                                                  | `0.016,0.018,0.02` |
| `TRANSCRIPTION_PRICE` | USD-price for one minute of audio transcription. Source: https://openai.com/pricing                                                                                                                                                                                                                                                                                                       | `0.006`            |
| `VISION_TOKEN_PRICE`  | USD-price per 1K tokens of image interpretation. Source: https://openai.com/pricing                                                                                                                                                                                                                                                                                                       | `0.01`             |
| `TTS_PRICES`          | A comma-separated list with prices for the tts models: `tts-1`, `tts-1-hd`. Source: https://openai.com/pricing                                                                                                                                                                                                                                                                            | `0.015,0.030`      |

Check out the [Budget Manual](https://github.com/n3d1117/chatgpt-telegram-bot/discussions/184) for possible budget configurations.

#### Additional optional configuration options
| Parameter                           | Description                                                                                                                                                                                                                                                                             | Default value                      |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
| `ENABLE_QUOTING`                    | Whether to enable message quoting in private chats                                                                                                                                                                                                                                      | `true`                             |
| `ENABLE_IMAGE_GENERATION`           | Whether to enable image generation via the `/image` command                                                                                                                                                                                                                             | `true`                             |
| `ENABLE_TRANSCRIPTION`              | Whether to enable transcriptions of audio and video messages                                                                                                                                                                                                                            | `true`                             |
| `ENABLE_TTS_GENERATION`             | Whether to enable text to speech generation via the `/tts`                                                                                                                                                                                                                              | `true`                             |
| `ENABLE_VISION`                     | Whether to enable vision capabilities in supported models                                                                                                                                                                                                                               | `true`                             |
| `PROXY`                             | Proxy to be used for OpenAI and Telegram bot (e.g. `http://localhost:8080`)                                                                                                                                                                                                             | -                                  |
| `OPENAI_PROXY`                      | Proxy to be used only for OpenAI (e.g. `http://localhost:8080`)                                                                                                                                                                                                                         | -                                  |
| `TELEGRAM_PROXY`                    | Proxy to be used only for Telegram bot (e.g. `http://localhost:8080`)                                                                                                                                                                                                                   | -                                  |
| `OPENAI_MODEL`                      | The OpenAI model to use for generating responses. You can find all available models [here](https://platform.openai.com/docs/models/)                                                                                                                                                    | `gpt-3.5-turbo`                    |
| `OPENAI_BASE_URL`                   | Endpoint URL for unofficial OpenAI-compatible APIs (e.g., LocalAI or text-generation-webui)                                                                                                                                                                                             | Default OpenAI API URL             |
| `ASSISTANT_PROMPT`                  | A system message that sets the tone and controls the behavior of the assistant                                                                                                                                                                                                          | `You are a helpful assistant.`     |
| `SHOW_USAGE`                        | Whether to show OpenAI token usage information after each response                                                                                                                                                                                                                      | `false`                            |
| `STREAM`                            | Whether to stream responses. **Note**: incompatible, if enabled, with `N_CHOICES` higher than 1                                                                                                                                                                                         | `true`                             |
| `MAX_TOKENS`                        | Upper bound on how many tokens the ChatGPT API will return                                                                                                                                                                                                                              | `1200` for GPT-3, `2400` for GPT-4 |
| `VISION_MAX_TOKENS`                 | Upper bound on how many tokens vision models will return                                                                                                                                                                                                                                | `300` for gpt-4-vision-preview     |
| `VISION_MODEL`                      | The Vision to Speech model to use. Allowed values: `gpt-4-vision-preview`                                                                                                                                                                                                               | `gpt-4-vision-preview`             |
| `ENABLE_VISION_FOLLOW_UP_QUESTIONS` | If true, once you send an image to the bot, it uses the configured VISION_MODEL until the conversation ends. Otherwise, it uses the OPENAI_MODEL to follow the conversation. Allowed values: `true` or `false`                                                                          | `true`                             |
| `MAX_HISTORY_SIZE`                  | Max number of messages to keep in memory, after which the conversation will be summarised to avoid excessive token usage                                                                                                                                                                | `15`                               |
| `MAX_CONVERSATION_AGE_MINUTES`      | Maximum number of minutes a conversation should live since the last message, after which the conversation will be reset                                                                                                                                                                 | `180`                              |
| `VOICE_REPLY_WITH_TRANSCRIPT_ONLY`  | Whether to answer to voice messages with the transcript only or with a ChatGPT response of the transcript                                                                                                                                                                               | `false`                            |
| `VOICE_REPLY_PROMPTS`               | A semicolon separated list of phrases (i.e. `Hi bot;Hello chat`). If the transcript starts with any of them, it will be treated as a prompt even if `VOICE_REPLY_WITH_TRANSCRIPT_ONLY` is set to `true`                                                                                 | -                                  |
| `VISION_PROMPT`                     | A phrase (i.e. `What is in this image`). The vision models use it as prompt to interpret a given image. If there is caption in the image sent to the bot, that supersedes this parameter                                                                                                | `What is in this image`            |
| `N_CHOICES`                         | Number of answers to generate for each input message. **Note**: setting this to a number higher than 1 will not work properly if `STREAM` is enabled                                                                                                                                    | `1`                                |
| `TEMPERATURE`                       | Number between 0 and 2. Higher values will make the output more random                                                                                                                                                                                                                  | `1.0`                              |
| `PRESENCE_PENALTY`                  | Number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far                                                                                                                                                                        | `0.0`                              |
| `FREQUENCY_PENALTY`                 | Number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far                                                                                                                                                                   | `0.0`                              |
| `IMAGE_FORMAT`                      | The Telegram image receive mode. Allowed values: `document` or `photo`                                                                                                                                                                                                                  | `photo`                            |
| `IMAGE_MODEL`                       | The DALL·E model to be used. Available models: `dall-e-2` and `dall-e-3`, find current available models [here](https://platform.openai.com/docs/models/dall-e)                                                                                                                          | `dall-e-2`                         |
| `IMAGE_QUALITY`                     | Quality of DALL·E images, only available for `dall-e-3`-model. Possible options: `standard` or `hd`, beware of [pricing differences](https://openai.com/pricing#image-models).                                                                                                          | `standard`                         |
| `IMAGE_STYLE`                       | Style for DALL·E image generation, only available for `dall-e-3`-model. Possible options: `vivid` or `natural`. Check availbe styles [here](https://platform.openai.com/docs/api-reference/images/create).                                                                              | `vivid`                            |
| `IMAGE_SIZE`                        | The DALL·E generated image size. Must be `256x256`, `512x512`, or `1024x1024` for dall-e-2. Must be `1024x1024` for dall-e-3 models.                                                                                                                                                    | `512x512`                          |
| `VISION_DETAIL`                     | The detail parameter for vision models, explained [Vision Guide](https://platform.openai.com/docs/guides/vision). Allowed values: `low` or `high`                                                                                                                                       | `auto`                             |
| `GROUP_TRIGGER_KEYWORD`             | If set, the bot in group chats will only respond to messages that start with this keyword                                                                                                                                                                                               | -                                  |
| `IGNORE_GROUP_TRANSCRIPTIONS`       | If set to true, the bot will not process transcriptions in group chats                                                                                                                                                                                                                  | `true`                             |
| `IGNORE_GROUP_VISION`               | If set to true, the bot will not process vision queries in group chats                                                                                                                                                                                                                  | `true`                             |
| `BOT_LANGUAGE`                      | Language of general bot messages. Currently available: `en`, `de`, `ru`, `tr`, `it`, `fi`, `es`, `id`, `nl`, `zh-cn`, `zh-tw`, `vi`, `fa`, `pt-br`, `uk`, `ms`, `uz`, `ar`.  [Contribute with additional translations](https://github.com/n3d1117/chatgpt-telegram-bot/discussions/219) | `en`                               |
| `WHISPER_PROMPT`                    | To improve the accuracy of Whisper's transcription service, especially for specific names or terms, you can set up a custom message.  [Speech to text - Prompting](https://platform.openai.com/docs/guides/speech-to-text/prompting)                                                    | `-`                                |
| `TTS_VOICE`                         | The Text to Speech voice to use. Allowed values: `alloy`, `echo`, `fable`, `onyx`, `nova`, or `shimmer`                                                                                                                                                                                 | `alloy`                            |
| `TTS_MODEL`                         | The Text to Speech model to use. Allowed values: `tts-1` or `tts-1-hd`                                                                                                                                                                                                                  | `tts-1`                            |

Check out the [official API reference](https://platform.openai.com/docs/api-reference/chat) for more details.

#### Functions
| Parameter                         | Description                                                                                                                                      | Default value                       |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| `ENABLE_FUNCTIONS`                | Whether to use functions (aka plugins). You can read more about functions [here](https://openai.com/blog/function-calling-and-other-api-updates) | `true` (if available for the model) |
| `FUNCTIONS_MAX_CONSECUTIVE_CALLS` | Maximum number of back-to-back function calls to be made by the model in a single response, before displaying a user-facing message              | `10`                                |
| `PLUGINS`                         | List of plugins to enable (see below for a full list), e.g: `PLUGINS=wolfram,weather`                                                            | -                                   |
| `SHOW_PLUGINS_USED`               | Whether to show which plugins were used for a response                                                                                           | `false`                             |

#### Available plugins
| Name                      | Description                                                                                                                                         | Required environment variable(s)                                     | Dependency          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|---------------------|
| `weather`                 | Daily weather and 7-day forecast for any location (powered by [Open-Meteo](https://open-meteo.com))                                                 | -                                                                    |                     |
| `wolfram`                 | WolframAlpha queries (powered by [WolframAlpha](https://www.wolframalpha.com))                                                                      | `WOLFRAM_APP_ID`                                                     | `wolframalpha`      |
| `ddg_web_search`          | Web search (powered by [DuckDuckGo](https://duckduckgo.com))                                                                                        | -                                                                    | `duckduckgo_search` |
| `ddg_translate`           | Translate text to any language (powered by [DuckDuckGo](https://duckduckgo.com))                                                                    | -                                                                    | `duckduckgo_search` |       
| `ddg_image_search`        | Search image or GIF (powered by [DuckDuckGo](https://duckduckgo.com))                                                                               | -                                                                    | `duckduckgo_search` |
| `crypto`                  | Live cryptocurrencies rate (powered by [CoinCap](https://coincap.io)) - by [@stumpyfr](https://github.com/stumpyfr)                                 | -                                                                    |                     |
| `spotify`                 | Spotify top tracks/artists, currently playing song and content search (powered by [Spotify](https://spotify.com)). Requires one-time authorization. | `SPOTIFY_CLIENT_ID`, `SPOTIFY_CLIENT_SECRET`, `SPOTIFY_REDIRECT_URI` | `spotipy`           |
| `worldtimeapi`            | Get latest world time (powered by [WorldTimeAPI](https://worldtimeapi.org/)) - by [@noriellecruz](https://github.com/noriellecruz)                  | `WORLDTIME_DEFAULT_TIMEZONE`                                         |                     |
| `dice`                    | Send a dice in the chat!                                                                                                                            | -                                                                    |                     |
| `youtube_audio_extractor` | Extract audio from YouTube videos                                                                                                                   | -                                                                    | `pytube`            |
| `deepl_translate`         | Translate text to any language (powered by [DeepL](https://deepl.com)) - by [@LedyBacer](https://github.com/LedyBacer)                              | `DEEPL_API_KEY`                                                      |                     |
| `gtts_text_to_speech`     | Text to speech (powered by Google Translate APIs)                                                                                                   | -                                                                    | `gtts`              |
| `whois`                   | Query the whois domain database - by [@jnaskali](https://github.com/jnaskali)                                                                       | -                                                                    | `whois`             |
| `webshot`                 | Screenshot a website from a given url or domain name - by [@noriellecruz](https://github.com/noriellecruz)                                          | -                                                                    |                     |
| `auto_tts`                | Text to speech using OpenAI APIs - by [@Jipok](https://github.com/Jipok)                                                                            | -                                                                    |                     |

#### Environment variables
| Variable                          | Description                                                                                                                                                                                     | Default value                       |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| `WOLFRAM_APP_ID`                  | Wolfram Alpha APP ID (required only for the `wolfram` plugin, you can get one [here](https://products.wolframalpha.com/simple-api/documentation))                                               | -                                   |
| `SPOTIFY_CLIENT_ID`               | Spotify app Client ID (required only for the `spotify` plugin, you can find it on the [dashboard](https://developer.spotify.com/dashboard/))                                                    | -                                   |
| `SPOTIFY_CLIENT_SECRET`           | Spotify app Client Secret (required only for the `spotify` plugin, you can find it on the [dashboard](https://developer.spotify.com/dashboard/))                                                | -                                   |
| `SPOTIFY_REDIRECT_URI`            | Spotify app Redirect URI (required only for the `spotify` plugin, you can find it on the [dashboard](https://developer.spotify.com/dashboard/))                                                 | -                                   |
| `WORLDTIME_DEFAULT_TIMEZONE`      | Default timezone to use, i.e. `Europe/Rome` (required only for the `worldtimeapi` plugin, you can get TZ Identifiers from [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)) | -                                   |
| `DUCKDUCKGO_SAFESEARCH`           | DuckDuckGo safe search (`on`, `off` or `moderate`) (optional, applies to `ddg_web_search` and `ddg_image_search`)                                                                               | `moderate`                          |
| `DEEPL_API_KEY`                   | DeepL API key (required for the `deepl` plugin, you can get one [here](https://www.deepl.com/pro-api?cta=header-pro-api))                                                                       | -                                   |

### Installing
Clone the repository and navigate to the project directory:

```shell
git clone https://github.com/n3d1117/chatgpt-telegram-bot.git
cd chatgpt-telegram-bot
```

#### From Source
1. Create a virtual environment:
```shell
python -m venv venv
```

2. Activate the virtual environment:
```shell
# For Linux or macOS:
source venv/bin/activate

# For Windows:
venv\Scripts\activate
```

3. Install the dependencies using `requirements.txt` file:
```shell
pip install -r requirements.txt
```

4. Use the following command to start the bot:
```
python bot/main.py
```

#### Using Docker Compose

Run the following command to build and run the Docker image:
```shell
docker compose up
```

#### Ready-to-use Docker images
You can also use the Docker image from [Docker Hub](https://hub.docker.com/r/n3d1117/chatgpt-telegram-bot):
```shell
docker pull n3d1117/chatgpt-telegram-bot:latest
docker run -it --env-file .env n3d1117/chatgpt-telegram-bot
```

or using the [GitHub Container Registry](https://github.com/n3d1117/chatgpt-telegram-bot/pkgs/container/chatgpt-telegram-bot/):

```shell
docker pull ghcr.io/n3d1117/chatgpt-telegram-bot:latest
docker run -it --env-file .env ghcr.io/n3d1117/chatgpt-telegram-bot
```

#### Docker manual build
```shell
docker build -t chatgpt-telegram-bot .
docker run -it --env-file .env chatgpt-telegram-bot
```

## Credits
- [ChatGPT](https://chat.openai.com/chat) from [OpenAI](https://openai.com)
- [python-telegram-bot](https://python-telegram-bot.org)
- [jiaaro/pydub](https://github.com/jiaaro/pydub)

## Disclaimer
This is a personal project and is not affiliated with OpenAI in any way.

## License
This project is released under the terms of the GPL 2.0 license. For more information, see the [LICENSE](LICENSE) file included in the repository.
