<div align="center">

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=banner&utm_campaign=awesome-claude-fable-5.2-video-prompts"><img src="assets/banner.jpg" alt="Awesome Claude Fable 5.2 影片提示詞" width="100%"></a>

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey)](LICENSE)
[![Prompts](https://img.shields.io/badge/Prompts-22_cases-111111)](README_zh-TW.md#menu)
[![Try Claude Fable 5.2 on APIKO](https://img.shields.io/badge/Try_Claude_Fable_5.2-on_APIKO-4F46E5)](https://apiko.app/zh-tw/models/claude-fable-5-2?utm_source=github&utm_medium=badge&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=model_try)
[![Claude Fable 5.2 API docs](https://img.shields.io/badge/Claude_Fable_5.2-API_docs-111111)](https://apiko.app/zh-tw/docs/api-manual/text-series/claude?utm_source=github&utm_medium=badge&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=docs)

[![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8_English-Default-4F46E5)](README.md)
[![🇨🇳 简体中文](https://img.shields.io/badge/%F0%9F%87%A8%F0%9F%87%B3_%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-%E6%9F%A5%E7%9C%8B-4F46E5)](README_zh-CN.md)
[![🇹🇼 繁體中文](https://img.shields.io/badge/%F0%9F%87%B9%F0%9F%87%BC_%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-Current-111111)](README_zh-TW.md)
[![🇰🇷 한국어](https://img.shields.io/badge/%F0%9F%87%B0%F0%9F%87%B7_%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%B3%B4%EA%B8%B0-4F46E5)](README_ko.md)

</div>

# Awesome Claude Fable 5.2 影片提示詞

<a id="introduction"></a>
## 🌟 簡介

**Claude Fable 5.2 影片提示詞：22 條真實提示詞和它們做出的影片，從 WebGL 滑桿、Three.js 場景到 Blender 動畫和 LilyPond 音樂。**

Claude Fable 5.2 影片提示詞，收集自發表後頭幾天創作者公開的作品。每張卡片都有作者原文提示詞和它做出的影片，可以直接複製對照。

線上搜尋與篩選： [apiko.app/claude-fable-5-2-video-prompts](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=readme&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=intro).

> [!NOTE]
> 提示詞保持作者發布時的原文，所以大多是英文；標題與簡介由我們撰寫。每則都署名作者並連結原帖。

<a id="quick-start"></a>
## 🚀 快速開始

**網頁上用：** 每則都有「在 APIKO 執行」連結，會在 [apiko.app](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=browser) 開啟這則範例；點「使用」，提示詞就會填進 Claude Fable 5.2 試用台。

**用 API：** 先建立 [APIKO API 金鑰](https://apiko.app/zh-tw/dashboard/apikeys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=api_key)，把提示詞送到 Messages API。Claude 回傳程式碼，在你的電腦上執行它來算出影片。

```bash
export APIKO_API_KEY="your_key_here"

curl -s https://api.apiko.app/v1/messages \
  -H "Authorization: Bearer $APIKO_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "Content-Type: application/json" \
  -d '{
  "model": "claude-fable-5-2",
  "max_tokens": 16000,
  "messages": [{
    "role": "user",
    "content": "Write one self-contained index.html that animates a paper boat crossing a lake at sunrise for 10 seconds at 1920x1080, plus the Playwright and FFmpeg commands that render it to boat.mp4."
  }]
}' | python3 -c 'import json,sys; print("".join(b.get("text","") for b in json.load(sys.stdin)["content"]))'
```

介面: `POST https://api.apiko.app/v1/messages` (送出提示詞)

<a id="how-to-write"></a>
## ✍️ 怎麼寫 Claude Fable 5.2 影片提示詞

Claude Fable 5.2 輸出的是程式碼，不是影片檔。程式碼在你的電腦上算圖並逐格錄下來。先決定路線，並在提示詞裡寫明。

- **單一自包含頁面** · `單一 HTML + WebGL 或 Canvas + Web Audio +「不用任何函式庫」` — 兩張音量滑桿卡片要求一個頁面裡只用原生 WebGL2、Web Audio 和像素緩衝。這種頁面在瀏覽器打開就能錄影。
- **Three.js 加影格時鐘** · `場景 + 長度 + 尺寸 + 影格率 + window.renderAt(t)` — 體素巴黎那張卡要求提供 renderAt(t)，可以按固定影格率逐格擷取。影片要求精確、不能靠即時錄影時就這樣寫。
- **Remotion 或 HyperFrames** · `框架 + 長度 + 要賣什麼 + 專案目錄` — 預告片類卡片點名 HyperFrames 或 Remotion，並在專案裡執行，讓模型先讀真實的產品再寫片子。
- **Blender 和 LilyPond** · `工具 + 主題 + 算圖設定，或「只要程式碼區塊」` — 動畫短片在 Blender 裡用 Python 搭每個鏡頭；音樂卡片只要 LilyPond 程式碼。兩者都要在本機裝好對應工具，才能把程式碼變成影片。
- **每次都要寫清楚的** · `長度 + 解析度 + 影格率 + effort + 你提供的素材` — 寫了長度的卡片都拿到了對應長度。要說明你會提供哪些素材（歌曲、歌詞、專案目錄），這裡有四張卡片依賴它們。

**這些 Claude Fable 5.2 案例說明了什麼**

- **一句話可能就夠** UFO、Logo 揭幕和「只用程式碼」的發表片都只有一句話。長規格是為了精確的效果，例如 6,000 字的滑桿研究。
- **創作者報了成本** 兩個滑桿分別花了 $7.48 和 $8.43；自製發表片跑了 57 分鐘，按 API 價約 $21。長任務要留預算。
- **大工程要用 Agent 跑** 60 秒發表片呼叫了 Opus 5.5 子代理，犯罪題材遊戲跑了兩個多小時。這類要在 Claude Code 等 Agent 裡跑，不是一次 API 呼叫。
- **effort 有影響** 音樂卡片用 Extra High，巫師短片用 high，預告片用 medium。Fable 5.2 每次請求都會思考，預設是 high。
- **Opus 5.5 依然接近** 有兩位作者在兩個模型上跑了同一條提示詞，其中一位更喜歡 Opus 5.5 的結果。換模型前先用自己的點子比一比。

<a id="menu"></a>
## 📑 目錄

- [✨ 動態設計](#motion-graphics) (6)
  - [兩句話做一支告別 Opus 5.5 的作品集短片](#motion-graphics-01)
  - [粒子文字變成星系、雙螺旋，最後拼出你的名字](#motion-graphics-02)
  - [一根潛入海底世界的音量滑桿](#motion-graphics-03)
  - [從黑夜滑到清晨的溫馨小屋開關](#motion-graphics-04)
  - [鉻金屬質感的 3D Logo 揭幕](#motion-graphics-05)
  - [一句話 15 秒動態設計師作品集](#motion-graphics-06)
- [🚀 發表與宣傳](#product-launch) (4)
  - [呼叫 Opus 5.5 子代理做的 60 秒發表片](#product-launch-01)
  - [「做你自己的發表影片，只用程式碼」](#product-launch-02)
  - [用 HyperFrames 做的課程社群預告片](#product-launch-03)
  - [一條提示詞做出發表會質感的知識站宣傳片](#product-launch-04)
- [🎞️ 短片](#short-film) (4)
  - [蒸汽火車變形成機器人的 2D 動畫短片](#short-film-01)
  - [UFO 降落 51 區並和人類打招呼](#short-film-02)
  - [小巫師親手造出並發表 Fable 5.2](#short-film-03)
  - [劍齒虎捕獵，純程式碼動畫](#short-film-04)
- [• 3D 場景](#3d-scenes) (2)
  - [用 Blender 搭的古耶路撒冷沉浸式 3D 模型](#3d-scenes-01)
  - [1888 年的懸浮體素巴黎，逐格算圖](#3d-scenes-02)
- [• 遊戲](#games) (2)
  - [一次生成的 Three.js 3D 籃球遊戲](#games-01)
  - [80 年代邁阿密風格城市裡的開放世界遊戲](#games-02)
- [• 音樂](#music) (4)
  - [用 LilyPond 寫的 G 小調巴赫風格聖詠](#music-01)
  - [給歌和歌詞做的日語歌詞動態影片](#music-02)
  - [從一個點長成整個世界：著色器影片配程式合成音樂](#music-03)
  - [用 LilyPond 寫的完整巴赫風格管風琴賦格](#music-04)
- [❓ 常見問題](#faq)
- [🔗 相關連結](#related)

<a id="motion-graphics"></a>
## ✨ 動態設計

> 作品集短片、Logo 揭幕和介面開關，用 HTML、WebGL 和著色器畫出來。 · 6 則

<a id="motion-graphics-01"></a>
### 1. 兩句話做一支告別 Opus 5.5 的作品集短片

作者 [@kaif9998](https://x.com/kaif9998) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-01#motion-graphics-01)** · [原帖](https://x.com/kaif9998/status/2119903824848761287)

在 Claude Code 裡先要一段 15 秒告別影片，再補一句「做成作品集」。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-01#motion-graphics-01"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/motion-graphics-01.webp" width="560" alt="兩句話做一支告別 Opus 5.5 的作品集短片 – Claude Fable 5.2"></a>

**提示詞:**

```text
Claude Code , two prompts:

1. "make a 15 second animated video that says final goodbye to Opus 5.5 as Fable 5.2 is here and I switched to it"
2. "make the video like it's your showreel"
```

<a id="motion-graphics-02"></a>
### 2. 粒子文字變成星系、雙螺旋，最後拼出你的名字

作者 [@ici_dab](https://x.com/ici_dab) · 68 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-02#motion-graphics-02)** · [原帖](https://x.com/ici_dab/status/2119901910237098351)

一段開放需求：做一個最能震撼人、能直接分享的作品。結果是帶配樂的互動式粒子動畫。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-02#motion-graphics-02"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/motion-graphics-02.webp" width="560" alt="粒子文字變成星系、雙螺旋，最後拼出你的名字 – Claude Fable 5.2"></a>

**提示詞:**

```text
the prompt: "I need you to create the most impressive thing I can share with people when you launch. It needs to be embeddable in a post and i can preface it however you like. it needs to have a visceral impact on people to show what you can do and the range of capabilities. It should grab them quickly. Be amazingly clever about this."
```

<a id="motion-graphics-03"></a>
### 3. 一根潛入海底世界的音量滑桿

作者 [@N1njaCodex](https://x.com/N1njaCodex) · 11 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-03#motion-graphics-03)** · [原帖](https://x.com/N1njaCodex/status/2119883560937001387)

長規格說明：純 WebGL2 + Web Audio、不用任何函式庫的開關元件。作者說這次花了 $7.48。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-03#motion-graphics-03"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/motion-graphics-03.webp" width="560" alt="一根潛入海底世界的音量滑桿 – Claude Fable 5.2"></a>

**提示詞:**

```text
Make "Deep Dive Switch", No. 063 in a series of web material studies: a depth switch that goes from light to dark, from the sea's surface to the floor of the abyss. Build it as one self-contained page with no libraries: raw WebGL2, Web Audio and a 2D pixel buffer.

PAGE
- Editorial layout: a small kicker "Material Studies / No. 063 · WebGL + Web Audio", an italic serif title "Deep Dive Switch.", and a one-line caption.
- The switch sits centred and large. Below it go three readouts (Depth, Zone, Music), a hint line and a "Sound on/off" button.
- The whole page's colours (background, text, lines) follow the depth: pale aqua at the surface, near-black blue in the abyss.
- It must work at phone width.

THE SWITCH
- A pill-shaped switch in a moulded bezel: white glossy plastic at the surface, deep navy in the abyss.
  - A soft drop shadow falls on the page and fades to nothing before the canvas edge.
  - A slight inner shadow runs along the top of the track.
- Inside it is a 176×50 pixel-art cross-section of the sea.
  - Redraw it every frame on the CPU and show it with nearest sampling, never smoothed.
  - Use whole device pixels per scene pixel where there is room.
- The knob is a glass bathysphere: a vertical capsule of clear glass, a little taller than the track, drawn in a single full-canvas WebGL2 fragment shader.
  - It magnifies what is under it (about 1.28×) and bends it.
  - At its rim it splits R, G and B. A darker refraction band sits inside a bright edge, with a Fresnel tint and a faint aqua cast.
  - Two highlights: a long soft streak at the upper left and a small dot at the lower right.
  - Light gathers toward its foot, and it casts a soft shadow on the scene.
- Motion:
  - It follows the finger on a spring, lagging a little.
  - It stretches sideways with speed and squashes vertically to keep its volume.
  - It wobbles on a damped spring driven by its acceleration.
- Controls:
  - Drag the knob, or drag anywhere on the track.
  - Tap to send it to the other end; it travels there on its spring.
  - Arrow keys, Home/End and Space/Enter also work.
  - The switch has role="slider" with ARIA values.

THE SEA (left = shallow, right = deep; an original palette)
- Sprites are filled shapes stamped with an automatic 1-px outline and a light top / dark bottom.
- The sea floor, left to right:
  - a sandy beach with a sandcastle;
  - a reef plateau with rocks;
  - a drop-off into rocky deep water;
  - the abyssal floor rising again at the far right.
- Up top on the left is sky with a sun, two flapping gulls and a little red sailboat bobbing on animated waves with a foam line.
  - The surface is level over the shallows, then rises out of the picture toward the deep, so the view seems to sink.
- The shallows:
  - turquoise water with swaying slanted god rays and moving caustics on the sand;
  - branching corals in pink, orange and violet, brain corals, swaying sea grass;
  - an anemone with a little orange-and-white fish darting about it;
  - a sea turtle gliding back and forth, paddling;
  - a school of yellow fish circling over the reef that scatters away from the knob.
- The twilight zone:
  - the water darkens to deep blue;
  - three translucent jellyfish, pink and violet, pulse and trail wavy tentacles; they glow softly and pulse faster when the knob comes near;
  - every half minute a faint whale silhouette swims past in the background.
- The midnight zone:
  - a long swaying chain of glowing cyan-and-green beads (a siphonophore);
  - small dark lanternfish with blinking light spots;
  - marine snow drifting down.
- The abyssal floor:
  - a hydrothermal vent breathing bubbles;
  - an anglerfish with a rod and a glowing lure;
  - a treasure chest.

LIGHT AND THE DIVE
- Daylight falls off with depth and dims a little toward the floor. It is quantised and Bayer-dithered so the gradient steps like pixel art.
- Below the shallows the bathysphere's searchlight comes on: a stepped, dithered pool of light around the knob, with a blue haze scattered in the water.
- Inside the lens everything is shown lit.
- Behind the knob trail rising bubbles and, in the dark, sparks of blue bioluminescence.
- Glowing crescent echoes trail behind it: pale aqua in the shallows, cyan in the deep.
- The lure lights its own little pool.
- As the knob nears, the anglerfish turns and opens its toothy mouth wide, and its lure blazes.
- At the very bottom the chest lid swings open on glowing gold, and gold glints fly up from it.

SOUND — all synthesised live with Web Audio, original music
- 84 BPM, a four-bar loop in D minor (Dm7 · B♭maj7 · Gm7 · A7sus4), on one lookahead-scheduled clock with a little swing.
- Layers fade in and out with depth:
  0. The surface: waves (filtered noise swelling slowly) and gull cries. The moment you go under, a splash, and the waves drop to a dull underwater roar.
  1. The reef: a kalimba ostinato (sine with bright, quickly fading overtones, in a long reverb), with bubbles popping on the off-beats.
  2. A soft dub beat: a round kick, rim clicks into a dotted echo, a swung shaker, a deep bass.
  3. The twilight: slow detuned pads, a whale singing now and then (a gliding, vibrato tone through a formant filter), then sonar pings ringing in the echo.
  4. The abyss: a breathing sub drone, a slow lub-dub heartbeat, and glassy arpeggios of high pentatonic notes ringing in the echo.
- The music sits behind a gentle low-pass that closes a little with depth, about 5 dB under the switch's own sounds.
- Switch sounds:
  - a bubble bloop when grabbed, a plop when released;
  - a water swish and bubble pops that grow with drag speed;
  - a splash crossing the surface either way;
  - a glass chime past each jellyfish;
  - the angler's deep gulp;
  - a fanfare when the chest opens: a rising kalimba arpeggio, a low boom and a shimmer.
- Audio starts on the first touch; a Sound on/off button.

READOUTS
- Depth, 0 → 6,000 m, mapped to the zones.
- Zone: Surface / Sunlit / Twilight / Midnight / Abyss.
- Music: Waves / Kalimba / Reef dub / Whale song / Sonar / Abyss.
```

<a id="motion-graphics-04"></a>
### 4. 從黑夜滑到清晨的溫馨小屋開關

作者 [@vib3coded](https://x.com/vib3coded) · 13 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-04#motion-graphics-04)** · [原帖](https://x.com/vib3coded/status/2119876781700505627)

同一套「材質研究」格式，單頁 WebGL2 + Web Audio。作者說用了 10 分鐘、$8.43。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-04#motion-graphics-04"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/motion-graphics-04.webp" width="560" alt="從黑夜滑到清晨的溫馨小屋開關 – Claude Fable 5.2"></a>

**提示詞:**

```text
Make "Daybreak Switch", No. 062 in a series of web material studies: a night-to-morning toggle in its own original style, as a single self-contained page (no libraries; raw WebGL2 + Web Audio + a 2D pixel buffer). Editorial layout: a small "Material Studies / No. 062 · WebGL + Web Audio" kicker, an italic serif title "Daybreak Switch.", a one-line caption; the switch centred and large; below it readouts (Clock, Light, Music), a hint line and a "Sound on/off" button. The whole page's colours (background, text, lines) follow the switch from a dark dusk-indigo at night to a pale lavender-grey by day. Works at phone width.

THE SWITCH
- A pill-shaped switch in a moulded bezel: white glossy plastic by day, graphite by night. A soft drop shadow falls on the page and fades to nothing before the canvas edge, with a slight inner shadow along the top of the track.
- Inside, a 176×50 pixel-art room, redrawn every frame on the CPU and shown with nearest sampling, never smoothed. Whole device pixels per scene pixel where there is room.
- The knob is a vertical capsule of clear jelly glass, a little taller than the track, drawn in one full-canvas WebGL2 fragment shader:
  - it magnifies (~1.28×) and bends the pixels under it;
  - it splits R/G/B at its rim, with a darker refraction band, a bright edge and a Fresnel tint;
  - two highlights: a long soft streak at the upper left and a small dot at the lower right;
  - light focused toward its foot, and a soft shadow on the room.
- The knob lags the finger on a spring, stretches horizontally with speed (squashing vertically to keep its volume), and wobbles on a damped spring fed by its acceleration.
- Inside the knob the room is always shown fully lit: the glass carries the morning.
- Controls: drag the knob or drag anywhere on the track; tap to toggle to the other end (it travels there on its spring); arrow keys, Home/End, Space/Enter; role="slider" with aria values.

THE ROOM (original, cosy palette)
Built from filled shapes stamped with an automatic 1-px outline and a light top / dark bottom, so every object reads as a pixel sprite:
- butter-yellow diamond wallpaper, teal wainscot, plank floor, a coral/cream/teal striped rug;
- a big window with curtains over a town of roofs;
- a shelf of coloured jelly jars and books, a potted plant;
- a brass floor lamp with a mint shade;
- a red boombox on a wooden cabinet, a framed picture of a little jelly shark, a round wall clock, a blue panelled door;
- a string of coloured bulbs sagging across the ceiling;
- a purple pet bed under the window.

LIGHT AND THE MORNING
- The knob drags the dawn across the room: left of it is day, right of it still night (indigo ambient). The edge dissolves in a 4×4 Bayer dither, with a warm dawn band just behind the knob.
- The window sky runs from night (navy, twinkling stars, a crescent moon, lit town windows) through dawn (violet to peach, the sun coming up) to day (blue, sun high, clouds drifting).
- Moonlight shafts through the window at night, warm sun shafts by day.
- The lamp clicks on early and casts a banded warm pool.
- Each ceiling bulb lights as the knob passes it, with a coloured dithered glow.
- Disco spots sweep the room at the party.
- The wall clock runs from 02:00 to 10:00.

THE STORY, BY POSITION
- An orange tabby cat:
  - asleep, curled in its bed, breathing, with z's rising;
  - awake, lying with its head up and blinking;
  - sitting up;
  - standing and walking out onto the rug;
  - at the end dancing on its hind legs to the beat, in sunglasses, with pink ghost trails.
- The plant sways and the boombox speakers thump with the beat; music notes float up from the boombox.
- A disco ball comes down from the ceiling; confetti sparkles fall.
- Glowing crescent echoes (coral to pink) trail behind the moving knob.
- Near the end (from about 08:24 on the clock) a puppy waits outside: warm light shows under the door with the shadows of its shifting paws, and it knocks. On each knock the door jolts 2 px, arcs of sound spring off it, and a "!" pops up over the cat; the knocking repeats every ~2.8 s until it's let in. At the very end the door swings open on a warm orange hallway and a white puppy with brown ears comes in, bobbing to the beat.

SOUND — all synthesised live with Web Audio, original music
- 100 BPM, a four-bar loop in F (Fmaj7 · Am7 · Dm7 · B♭maj7), on one lookahead-scheduled clock with a little swing.
- Layers fade in by the knob's position:
  0. Night: crickets (AM-chirped sine trains) and soft wind.
  1. A music box arpeggiating the chords (bell partials, short room reverb).
  2. A lo-fi beat (kick, noise-and-tone snare, hats) and a round bass.
  3. Warm detuned pads and a square-wave tune with vibrato.
  4. The party: four on the floor, claps, open hats, sub bass, the rest of the mix pumping under the kick.
- The music sits behind a low-pass that opens with the dawn, and ~5 dB under the switch's own sounds.
- Switch sounds:
  - a glass tink plus a jelly blop when grabbed, a plop when released;
  - a band-passed noise rub following the drag speed;
  - a pentatonic pluck for every bulb lit (a glissando when you sweep across), softer and lower when one goes out;
  - the lamp's double click and a cat's "mrrp" (formant-filtered saw) when it wakes;
  - a riser and crash into the party, and a record-brake when you drag back out of the beat;
  - the puppy's yip when it comes in.
- The knock, like a real heavy door knock: three hits 0.25 s apart, panned toward the door. Each hit is a knuckle click (band-passed noise) over a deep thump that sags from ~98 to ~60 Hz over a quarter second, with quicker overtones (190→128 Hz, 410 Hz) and soft saturation so small speakers hear it. The music ducks to ~45% under each hit, and the knocks peak at 3–4× the music's level.
- Audio starts on the first touch; a Sound on/off button.
- Readouts: Clock (02:00–10:00), Light (Night / First light / Sunrise / Morning / Party), Music (Crickets / Music box / Beat / Band / Party).
```

<a id="motion-graphics-05"></a>
### 5. 鉻金屬質感的 3D Logo 揭幕

作者 [@hello_amani](https://x.com/hello_amani) · 36 秒 · 1:1 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-05#motion-graphics-05)** · [原帖](https://x.com/hello_amani/status/2119873980786237842)

一句話：用鉻金屬和網格做我的 Logo 3D 揭幕，多迭代幾輪。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-05#motion-graphics-05"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/motion-graphics-05.webp" width="560" alt="鉻金屬質感的 3D Logo 揭幕 – Claude Fable 5.2"></a>

**提示詞:**

```text
the prompt was: make my logo reveal in 3D with chromatic metal and grids
and bunch of iteration
```

<a id="motion-graphics-06"></a>
### 6. 一句話 15 秒動態設計師作品集

作者 [@himanshutwtxs](https://x.com/himanshutwtxs) · 15 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-06#motion-graphics-06)** · [原帖](https://x.com/himanshutwtxs/status/2120017106804900304)

很多人在 Opus 5.5 上跑過的同一句話，換成 Fable 5.2：緩動、字體、景深、節奏都在一支片裡。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=motion-graphics-06#motion-graphics-06"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/motion-graphics-06.webp" width="560" alt="一句話 15 秒動態設計師作品集 – Claude Fable 5.2"></a>

**提示詞:**

```text
make a dynamic 15-second motion graphics video that shows what an incredible motion designer you are, like it's your showreel for a résumé. go all out
```

<a id="product-launch"></a>
## 🚀 發表與宣傳

> 發表片和預告片，從一句「只用程式碼」到讓模型先調研整個專案目錄。 · 4 則

<a id="product-launch-01"></a>
### 7. 呼叫 Opus 5.5 子代理做的 60 秒發表片

作者 [@grafikcem](https://x.com/grafikcem) · 60 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-01#product-launch-01)** · [原帖](https://x.com/grafikcem/status/2119910525064937806)

土耳其語提示詞：在發表當天，用 Opus 5.5 子代理給 Fable 5.2 做一支 60 秒動畫宣傳片。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-01#product-launch-01"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/product-launch-01.webp" width="560" alt="呼叫 Opus 5.5 子代理做的 60 秒發表片 – Claude Fable 5.2"></a>

**提示詞:**

```text
Bugün duyurulmana özel Fable 5.2 modeli için opus 5.5 subagentları kullanarak kendine 60 saniyelik bir tanıtım animasyon filmi hazırla.
```

<a id="product-launch-02"></a>
### 8. 「做你自己的發表影片，只用程式碼」

作者 [@furkancavlakcom](https://x.com/furkancavlakcom) · 74 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-02#product-launch-02)** · [原帖](https://x.com/furkancavlakcom/status/2119896886345695521)

一句土耳其語。作者說用了 57 分鐘、按 API 價約 $21、1,702 行 Python、2,220 格，音樂也是合成的。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-02#product-launch-02"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/product-launch-02.webp" width="560" alt="「做你自己的發表影片，只用程式碼」 – Claude Fable 5.2"></a>

**提示詞:**

```text
Kendi lansman videonu yap. Sadece kodla.
```

<a id="product-launch-03"></a>
### 9. 用 HyperFrames 做的課程社群預告片

作者 [@midudev](https://x.com/midudev) · 32 秒 · 9:16 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-03#product-launch-03)** · [原帖](https://x.com/midudev/status/2119876297304203273)

西班牙語提示詞，在作者自己的專案裡執行：要有聲音、動畫要炸，medium 檔位，約 10 分鐘。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-03#product-launch-03"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/product-launch-03.webp" width="320" alt="用 HyperFrames 做的課程社群預告片 – Claude Fable 5.2"></a>

**提示詞:**

```text
El prompt:  Crea un trailer en video animado para compartir en redes sociales de este proyecto. Quiero que lo vendas de forma espectacular, que tenga sonido y animaciones brutales. Usa hyperframes.

Esfuerzo medio.
```

<a id="product-launch-04"></a>
### 10. 一條提示詞做出發表會質感的知識站宣傳片

作者 [@czzzzzzJ_](https://x.com/czzzzzzJ_) · 298 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-04#product-launch-04)** · [原帖](https://x.com/czzzzzzJ_/status/2120023093464682817)

在知識站專案目錄裡執行：先調研業務，只問一輪問題，然後直接成片，風格像蘋果發表會。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=product-launch-04#product-launch-04"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/product-launch-04.webp" width="560" alt="一條提示詞做出發表會質感的知識站宣傳片 – Claude Fable 5.2"></a>

**提示詞:**

```text
你现在在我的知识站项目目录下，完整地调研我知识站上所有的业务、提供的内容，以及我的商业模式。使用 opuscar这个库帮我生成我的知识站宣传视频，整体风格我希望是像苹果的发布会那种风格质感。素材可以自行搜索和获取截屏。关于我不了解的内容，DOC 文件夹下有我的个人介绍。在整个宣传片制作前，你有一次向我提问的机会，收集我的想法，然后我要求你直接成片。
```

<a id="short-film"></a>
## 🎞️ 短片

> 用程式碼說故事：Blender 日式動畫、Three.js 的 UFO、角色動畫和動物捕獵。 · 4 則

<a id="short-film-01"></a>
### 11. 蒸汽火車變形成機器人的 2D 動畫短片

作者 [@0kncn](https://x.com/0kncn) · 90 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-01#short-film-01)** · [原帖](https://x.com/0kncn/status/2119901782482543073)

長規格說明：全部在 Blender 裡用 Python 搭建，Eevee 算圖，再逐格描線上色，音樂自己合成。90 秒。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-01#short-film-01"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/short-film-01.webp" width="560" alt="蒸汽火車變形成機器人的 2D 動畫短片 – Claude Fable 5.2"></a>

**提示詞:**

```text
Create a 2D anime short. It must look completely like real Japanese anime, as if it were taken directly from a finished theatrical anime film. This is traditional-looking, hand-drawn 2D anime, not a 3D animation, a moving illustration, or a stylized web graphic.

Build everything in Blender from Python, render it in Eevee, then ink and paint every frame in a second pass. Deliver one 1920x1080, 24 fps MP4 with a synthesized soundtrack. Use any tools, libraries, references, guides, literally anything, as long as the final result looks 100% like hand-drawn 2D anime.

Use theatrical anime as the art style reference for the design, line work, painted backgrounds, color and atmosphere. The film is 90 seconds long (2160 frames), in 42 shots. Its hero is a steam locomotive that transforms into a robot. No people appear in the film.

HERO
No. 9, a 1940s 2-8-2 freight locomotive with a four-axle tender, 23 m long, asleep for decades in a mountain engine shed: matte black boiler with rust runs, faded red wheel centres and buffer beam, brass number plate "9", one large headlamp, two amber marker lamps, moss on the running boards, ivy through the cab windows, and a stork's nest on the cab roof. As a robot it stands 21 m tall with its shoulders at 17 m. It is an original design, not a character from any existing series. It moves on twos, slow and heavy. Its wheels never slip and its feet never slide.

TRANSFORM
One transformation, at full speed, 120 frames, in five stages of 24 frames. Every part is rigid: nothing stretches, nothing vanishes, nothing appears. Each part travels on a hinge or a slide you can see.
1. Legs: the tender uncouples, splits lengthwise and swings down; its two bogies lock as feet, the coal stays in bunkers on the calves.
2. Hips: the cab drops and widens into the pelvis; the trailing truck folds onto the lower back.
3. Torso: the boiler tilts upright, firebox at the waist, smokebox at the top; the chimney and steam dome end on the upper back and keep venting.
4. Arms: the running boards swing out with the cylinders as shoulders, the piston and connecting rods as forearms, and hands with three fingers and a thumb unfolding from the valve gear; the front driving wheels ride up as shoulder discs, the rear ones fold to hips and knees.
5. Head: the smokebox door hinges forward as the chest plate with the headlamp at its centre; a riveted helmet rises from the smokebox with one dark visor slit and the two marker lamps as amber eyes; the cowcatcher folds up as a collar.
The cab roof panel rides up to the right shoulder and carries the stork's nest, never tilted more than 10 degrees.
Stages 1-3 happen on the rails, with the first strides landing on the ballast either side of the track. Stages 4-5 happen in the air.

WORLD
A single-track mountain railway at real scale. At the top, an ore mine with a loading bunker and a rake of twelve four-wheel hopper wagons. The line descends through larch forest and a short rock tunnel to a viaduct: seven 18 m steel girder spans on stone piers, 126 m long, the deck 17 m above a turquoise meltwater river 3 m deep. Beyond it, a small station: a stone engine shed, a water tower, a semaphore signal with an alarm bell, a signal box, a siding ending in a sand drag. Snow peaks behind, a cliff face above the viaduct, telegraph poles along the whole line.

STORY
A clear spring morning in the valley. Meltwater loosens the cliff: a rockfall hits the middle pier of the viaduct, the pier collapses into the river and the two girders it carried sag into a V, held only by the rails. Up at the mine the shock snaps a coupling and the twelve loaded wagons start to roll downhill, unmanned. At the station the semaphore drops to danger and the bell rings. In the dark shed the firebox glows, the pressure needle climbs, the headlamp lights; the stork flies up. No. 9 bursts through the shed doors tearing ivy and rust, and charges up the grade with the wagons coming down the other side. On the approach it transforms at full speed, leaps from the abutment, lands crouched in the river, wades to the fallen pier, and lifts the sagging joint onto its shoulders and raised hands. The wagons hit the viaduct: it sinks 0.3 m as each one passes over and holds. The rake runs through the station into the sand drag and stops. No. 9 does not come back out. It locks its knees and stays as the new pier. The steam thins, the stork returns to its nest, the visor dims.

LIGHT
High-key anime light, never murky: a morning sun from the south-east, a saturated cobalt sky, white cumulus with lavender shadows, snow peaks with blue shadows, fresh green larch, a turquoise river with drawn white water. Light only changes with a cause you can see: rock dust dims the gorge for 3 seconds, steam whites out a frame, the firebox throws orange onto the shed walls. Cel light with hard shadows, gouache backgrounds, ink lines on every machine, rail and building, effects drawn on twos: steam as inked rolling shapes with a flat shadow tone, water as inked sheets with foam crowns, dust as drawn clouds, never particle mush.

SOUND
A synthesized orchestra on a 144 bpm grid: one beat is 10 frames, and every cut lands on a multiple of 5 frames. A hopeful theme on clarinet and horn, the collapse in E minor, a 12/8 chase with the exhaust chuff as percussion at four beats per wheel revolution, a heavy 3/4 for the hold with one low drum per wagon. 16 hits land exactly on the picture: the rockfall, the pier, the coupling, the signal arm, the shed doors, each transformation lock, the landing, the lift, the first and last wagon. The steam whistle is heard twice: once on waking, once on the hold.

FORMAT
Write the film as a Python story clock: one state per frame for every pose, camera, wheel angle, rod position, transformation part, wagon, effect and sound cue.

CHECKS
Before the final render a script tests every frame on the real meshes: no part of No. 9 goes through another part, in either form or at any frame of the transformation; the total volume of its parts is the same in both forms; every wheel on a rail turns exactly as far as it travels; planted feet do not move; No. 9 never goes through the track, the shed, the viaduct or the riverbed; the wagons stay on the rails and never touch each other except at the couplings; the camera never enters a mesh, the cliff or the water; nothing jumps between frames.
```

<a id="short-film-02"></a>
### 12. UFO 降落 51 區並和人類打招呼

作者 [@danteeonsol](https://x.com/danteeonsol) · 30 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-02#short-film-02)** · [原帖](https://x.com/danteeonsol/status/2119887623070077213)

一句話。作者說全部用 three.js + Remotion 寫成，沒有外部模型、貼圖和素材音效。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-02#short-film-02"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/short-film-02.webp" width="560" alt="UFO 降落 51 區並和人類打招呼 – Claude Fable 5.2"></a>

**提示詞:**

```text
make me a 30 second video of a UFO visiting Area 51 and greeting humans, ultra detailed, cinematic lighting
```

<a id="short-film-03"></a>
### 13. 小巫師親手造出並發表 Fable 5.2

作者 [@other__reality](https://x.com/other__reality) · 26 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-03#short-film-03)** · [原帖](https://x.com/other__reality/status/2119885430627913784)

high 檔位，在作者已有的動畫底稿上執行，重現時需要一個類似的起始專案。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-03#short-film-03"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/short-film-03.webp" width="560" alt="小巫師親手造出並發表 Fable 5.2 – Claude Fable 5.2"></a>

**提示詞:**

```text
Create an animated video of clawd creating and releasing Claude Fable 5.2
```

<a id="short-film-04"></a>
### 14. 劍齒虎捕獵，純程式碼動畫

作者 [@wshuyi](https://x.com/wshuyi) · 28 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-04#short-film-04)** · [原帖](https://x.com/wshuyi/status/2120014892040417720)

中文提示詞：不用任何技能，純程式動畫，音效自己用程式產生，30 秒以內。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=short-film-04#short-film-04"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/short-film-04.webp" width="560" alt="劍齒虎捕獵，純程式碼動畫 – Claude Fable 5.2"></a>

**提示詞:**

```text
不使用任何技能，做一段纯编程形成的动画视频：剑齿虎的捕猎。不用配音，你自己编程生成音效，时长控制在 30 秒以内
```

<a id="3d-scenes"></a>
## • 3D 場景

> 在 Blender 或 Three.js 裡搭出一整個地方，再用鏡頭巡遊展示。 · 2 則

<a id="3d-scenes-01"></a>
### 15. 用 Blender 搭的古耶路撒冷沉浸式 3D 模型

作者 [@kplikethebird](https://x.com/kplikethebird) · 30 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=3d-scenes-01#3d-scenes-01)** · [原帖](https://x.com/kplikethebird/status/2119900775727902732)

一句話，要求按史實還原某一週的整座城市。成片巡遊了聖殿、庭園和宮殿。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=3d-scenes-01#3d-scenes-01"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/3d-scenes-01.webp" width="560" alt="用 Blender 搭的古耶路撒冷沉浸式 3D 模型 – Claude Fable 5.2"></a>

**提示詞:**

```text
Build an immersive, historically accurate 3D model of Jerusalem during the week of Jesus's final visit using Blender.
```

<a id="3d-scenes-02"></a>
### 16. 1888 年的懸浮體素巴黎，逐格算圖

作者 [@RezAIT00](https://x.com/RezAIT00) · 14 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=3d-scenes-02#3d-scenes-02)** · [原帖](https://x.com/RezAIT00/status/2119894257519767656)

詳細的 three.js 規格，提供 renderAt(t) 方便逐格擷取：浮島上的巴黎，艾菲爾鐵塔正在興建。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=3d-scenes-02#3d-scenes-02"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/3d-scenes-02.webp" width="560" alt="1888 年的懸浮體素巴黎，逐格算圖 – Claude Fable 5.2"></a>

**提示詞:**

```text
Build a single self-contained three.js HTML page that renders a 14-second animation (1280x720, 30fps, deterministic: expose window.renderAt(t) so every frame can be captured).  Scene: a floating voxel diorama island - Paris, 1888, the Eiffel Tower under construction. Everything is already moving on frame 1.  Island: - floating chunk with layered rock underside, the Seine curving across the front with stone quays and an arched bridge - Champ de Mars: dirt work yard, stacks of iron girders, wooden sheds, a steam engine with a smoking chimney - around it: rows of Haussmann buildings with cream walls, grey zinc roofs, chimneys, tiny trees along the boulevards  The tower (the hero): - dark reddish-brown wrought iron lattice made of thin voxel beams with real X-bracing, not solid blocks - four curved legs and the first platform finished, the second level half built, the top section only a skeleton - wooden scaffolding towers under the legs, small creeper cranes on the structure lifting girders on chains - glowing orange rivet sparks where workers hammer, small puffs of steam  Life (hundreds of tiny voxel people, ~3 voxels tall): - riveting teams on every level with hammers swinging, workers walking along beams - girders hoisted by cranes swinging slowly into place - horse-drawn carts carrying iron across the yard, crowds of onlookers in 1880s clothes with top hats and parasols - a riverboat with a smoking funnel moving along the Seine, carriages crossing the bridge, pigeons circling the tower  Camera and look: - wide view of the whole island, slow orbit (~25 degrees) with a gentle push-in toward the tower - warm late-afternoon sun, soft shadows, ambient occlusion, light haze, rounded voxels, ACES tone mapping, soft bloom on sparks

Full credits go to @semichenkko for this prompt
```

<a id="games"></a>
## • 遊戲

> 一條提示詞做出的 Three.js 可玩遊戲，影片是試玩錄影。 · 2 則

<a id="games-01"></a>
### 17. 一次生成的 Three.js 3D 籃球遊戲

作者 [@joshvlc](https://x.com/joshvlc) · 19 秒 · 21:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=games-01#games-01)** · [原帖](https://x.com/joshvlc/status/2119894656221958575)

直白列出規則和操作：運球、跳投、灌籃、抄截、傳球、兩支隊。一次成型。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=games-01#games-01"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/games-01.webp" width="560" alt="一次生成的 Three.js 3D 籃球遊戲 – Claude Fable 5.2"></a>

**提示詞:**

```text
Can you make a 3D basketball game using THREE.js? It should have a player in two different colored uniforms for the two teams and should follow the basic rules of basketball. It should have basic funcionality:
- dribble (happens automatically when player runs)
- shoot (hold for jump shot); dunk automatically near rim; jump/block if you don't have the ball
- steal
- pass to teammate
- 1 player: the teammates should be CPU and play normally (they should get open for you) and the player always controls the person with the ball (if someone on their team has it); the other team should be CPU controlled
- fouls + penalty shots
- the game should start on a tip (hit shoot button to tip)
Note: include sound effects and crowd cheering! You can use Blender (installed on this machine) if needed for the graphics!
```

<a id="games-02"></a>
### 18. 80 年代邁阿密風格城市裡的開放世界遊戲

作者 [@ericmaskfr](https://x.com/ericmaskfr) · 135 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=games-02#games-02)** · [原帖](https://x.com/ericmaskfr/status/2119910195325481026)

一條提示詞定好循環：走路、打鬥、偷車、被追、賺錢花錢。作者說用了 2 小時 14 分鐘。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=games-02#games-02"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/games-02.webp" width="560" alt="80 年代邁阿密風格城市裡的開放世界遊戲 – Claude Fable 5.2"></a>

**提示詞:**

```text
you're a senior game dev. build a third-person open-world crime game in a sunny 80s miami-style city. make the loop tight: walk, fight, steal a car, get chased, earn money, spend it. every system feeds the next: crimes bring heat, heat brings cops, missions pay, money unlocks the garage. cars need weight: gears, skids, real crashes. the city has to feel alive with traffic, people and day into night. no audio files, generate every sound in code. after each system, play it yourself, screenshot it and fix what looks wrong. don't stop until a stranger could play for 10 minutes without hitting a bug
```

<a id="music"></a>
## • 音樂

> 用 LilyPond 寫的樂譜，以及配程式合成音樂的歌詞影片和著色器影片。 · 4 則

<a id="music-01"></a>
### 19. 用 LilyPond 寫的 G 小調巴赫風格聖詠

作者 [@aug5thmusic](https://x.com/aug5thmusic) · 45 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-01#music-01)** · [原帖](https://x.com/aug5thmusic/status/2119879319426404780)

Extra High 檔位，只要程式碼區塊。做巴赫評測的作者說這是目前看過最好的聖詠之一。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-01#music-01"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/music-01.webp" width="560" alt="用 LilyPond 寫的 G 小調巴赫風格聖詠 – Claude Fable 5.2"></a>

**提示詞:**

```text
Prompt: “In LilyPond (version 2.24), write a 4-part chorale in the style of Bach, 3/4 time, G minor. Use two staves -- soprano and alto on the top staff, tenor and bass on the bottom staff. Respond with only the code block.” (Extra High effort)
```

<a id="music-02"></a>
### 20. 給歌和歌詞做的日語歌詞動態影片

作者 [@takamasa045](https://x.com/takamasa045) · 53 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-02#music-02)** · [原帖](https://x.com/takamasa045/status/2120014216753262816)

日語提示詞：當成作品集來秀一手動態設計，約 1 分鐘。作者提供了歌曲和歌詞，並和 Opus 5.5 做了比較。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-02#music-02"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/music-02.webp" width="560" alt="給歌和歌詞做的日語歌詞動態影片 – Claude Fable 5.2"></a>

**提示詞:**

```text
自分がどれほど優れたモーションデザイナーか、ポートフォリオ作品のつもりで披露せよ。ツールも技術も自由。大胆なアートディレクションと力強いモーションで、1秒も無駄にするな。まずは1分くらい
```

<a id="music-03"></a>
### 21. 從一個點長成整個世界：著色器影片配程式合成音樂

作者 [@tankazunori0914](https://x.com/tankazunori0914) · 64 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-03#music-03)** · [原帖](https://x.com/tankazunori0914/status/2120012834461646927)

日語提示詞：零素材、只用程式碼。作者說共 1,076 行，畫面全是著色器，音樂也用程式合成。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-03#music-03"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/music-03.webp" width="560" alt="從一個點長成整個世界：著色器影片配程式合成音樂 – Claude Fable 5.2"></a>

**提示詞:**

```text
Fable 5.2の実力を見せつける動画を作成して。
条件：素材ゼロ、コードだけで作る。hyperframesスキルの「暗い地・光・粒子は避ける」「音楽をコードで書かない」は今回は外してよい。
```

<a id="music-04"></a>
### 22. 用 LilyPond 寫的完整巴赫風格管風琴賦格

作者 [@aug5thmusic](https://x.com/aug5thmusic) · 125 秒 · 16:9 · **[▶ 在 APIKO 執行](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-04#music-04)** · [原帖](https://x.com/aug5thmusic/status/2119907891419480107)

Extra High 檔位的一句話。影片播放排好的樂譜和產生的音訊。

<a href="https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=case&utm_campaign=awesome-claude-fable-5.2-video-prompts&utm_content=music-04#music-04"><img src="https://media.apiko.app/prompts/claude-fable-5-2-video-prompts/music-04.webp" width="560" alt="用 LilyPond 寫的完整巴赫風格管風琴賦格 – Claude Fable 5.2"></a>

**提示詞:**

```text
In LilyPond (version 2.24), write a complete fugue for organ in the style of Bach.
```

<a id="faq"></a>
## ❓ 常見問題

<details>
<summary><b>Claude Fable 5.2 能做影片嗎？</b></summary>

它寫的是程式碼：HTML 頁面、Three.js 場景、Remotion 或 HyperFrames 專案、Blender 腳本或 LilyPond 樂譜。程式碼在你的電腦上算圖後錄成影片。

</details>

<details>
<summary><b>這些 Claude Fable 5.2 提示詞是原版嗎？</b></summary>

是。每條提示詞都和作者本人的貼文或回覆逐字核對過，每支影片都是作者為這條提示詞發的那一支，每張卡片都連結到出處。

</details>

<details>
<summary><b>這些 Claude Fable 5.2 提示詞能免費用嗎？成片歸誰？</b></summary>

提示詞和影片歸各卡片署名的創作者所有。可以當作起點，轉載前請看創作者的說明。

</details>

<details>
<summary><b>怎麼用 API 跑 Claude Fable 5.2 影片提示詞？</b></summary>

透過 Messages 或 Chat Completions 介面送給 claude-fable-5-2 模型，保存它回傳的程式碼。經 APIKO 呼叫時單次回覆最多輸出 32K token，大型專案要在 Agent 裡分多輪跑。

</details>

<details>
<summary><b>Claude Fable 5.2 用哪個 effort 檔位？</b></summary>

Anthropic 預設是 high，Fable 5.2 每次請求都會思考。這裡的音樂卡片用 Extra High；預告片用 medium，約 10 分鐘跑完。

</details>

<details>
<summary><b>為什麼我的 Claude Fable 5.2 結果和影片不一樣？</b></summary>

每次執行結果都會不同，作者也可能用了別的 effort 檔位、工具、既有專案或多輪修改。

</details>

<details>
<summary><b>Claude Fable 5.2 也能做音樂嗎？</b></summary>

有幾張卡片用 Web Audio 或 Python 在程式碼裡合成聲音。一支歌詞影片用的是作者自己的歌，LilyPond 卡片直接寫樂譜。

</details>

<details>
<summary><b>做影片該用 Claude Fable 5.2 還是 Claude Opus 5.5？</b></summary>

Anthropic 建議先用 Opus 5.5，遇到更難、更長的工作再換 Fable 5.2。我們的 Claude Opus 5.5 影片提示詞庫可以拿來比較。

</details>


<a id="related"></a>
## 🔗 相關連結

- [Claude Fable 5.2 影片提示詞 · apiko.app](https://apiko.app/zh-tw/claude-fable-5-2-video-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-claude-fable-5.2-video-prompts)
- [Claude Fable 5.2 模型頁](https://apiko.app/zh-tw/models/claude-fable-5-2?utm_source=github&utm_medium=related&utm_campaign=awesome-claude-fable-5.2-video-prompts)
- [Claude API 文件](https://apiko.app/zh-tw/docs/api-manual/text-series/claude?utm_source=github&utm_medium=related&utm_campaign=awesome-claude-fable-5.2-video-prompts)
- [Claude Opus 5.5 影片提示詞](https://apiko.app/zh-tw/claude-opus-5-5-video-prompts?utm_source=github&utm_medium=related&utm_campaign=awesome-claude-fable-5.2-video-prompts)
- [APIKO 對話](https://apiko.app/zh-tw/chat?utm_source=github&utm_medium=related&utm_campaign=awesome-claude-fable-5.2-video-prompts)
- [APIKO API 程式碼範例](https://github.com/tong0619453646-dev/apiko-ai-api-examples)

**更多提示詞合集**

- [Awesome Seedance 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome Seedance 2.0 Prompts](https://github.com/tong0619453646-dev/awesome-seedance-2.0-prompts/blob/main/README_zh-TW.md)
- [Awesome Kling 4.0 Prompts](https://github.com/tong0619453646-dev/awesome-kling-4.0-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.6 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.6-prompts/blob/main/README_zh-TW.md)
- [Awesome Nano Banana 2.1 Prompts](https://github.com/tong0619453646-dev/awesome-nano-banana-2.1-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2.5 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2.5-prompts/blob/main/README_zh-TW.md)
- [Awesome GPT Image 2 Prompts](https://github.com/tong0619453646-dev/awesome-gpt-image-2-prompts/blob/main/README_zh-TW.md)
- [Awesome Claude Opus 5.5 Video Prompts](https://github.com/tong0619453646-dev/awesome-claude-opus-5.5-video-prompts/blob/main/README_zh-TW.md)
- [Awesome Wan 3.0 Prompts](https://github.com/tong0619453646-dev/awesome-wan-3.0-prompts/blob/main/README_zh-TW.md)

<a id="license"></a>
## 📄 授權與出處

提示詞和影片歸各卡片署名的創作者所有，每張卡片都連結到原帖。標題、簡介、譯文與生成腳本採用 [CC BY 4.0](LICENSE) 授權。

如果這份合集幫你省了時間，按個 ⭐ 能讓更多人看到。
