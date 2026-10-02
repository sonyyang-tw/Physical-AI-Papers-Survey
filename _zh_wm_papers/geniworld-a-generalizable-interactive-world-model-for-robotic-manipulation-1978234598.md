---
layout: paper
title: "GeniWorld: A Generalizable Interactive World Model for Robotic Manipulation via Visual Actions"
section: wm
page_id: "1978234598"
permalink: /zh/wm/geniworld-a-generalizable-interactive-world-model-for-robotic-manipulation-1978234598/
---

### Abstract

通用機器人 policy 雖展現強大能力，但在複雜、未見過的環境中穩健性仍有限，而規模化真實世界資料收集與評測成本高昂且困難。既有 action-conditioned world model 提供一個有希望的替代方案——讓機器人能在「想像空間」中互動——但這類方法通常直接以數值動作向量（numerical action vector）條件化生成模型，存在兩個關鍵限制：其一，數值動作向量缺乏顯式空間對齊資訊，難以精確建模複雜機器人運動；其二，低維動作條件化將具身運動與環境變化糾纏在一起，迫使模型過度關注與互動無關的細節，導致對未見場景泛化能力不佳。本文提出 GeniWorld，一個以具身視覺動作（embodied visual actions）為條件的可泛化互動式 world model。作者以 URDF-based 渲染將數值動作序列轉換為視覺動作表示，實現具空間對齊的動作控制，並透過明確解耦具身運動學與環境動態，緩解場景過擬合問題並促進機器人-環境互動建模；同時建構一個結合高頻機器人運動學控制的自迴歸影片預測模型，實現與機器人 policy 及人類遠端操作者的閉環互動。實驗顯示，即使僅在有限的固定場景資料上訓練，GeniWorld 仍能取得優異的分布內表現，並對高度隨機化的未見環境展現穩健的零樣本泛化能力；作為下游應用，GeniWorld 可作為在環境擾動下依然可靠的可規模化 policy 評估器，且即使僅有限量真實示範，仍能在 world model 中生成多樣化操作軌跡，提升下游 policy 在複雜環境中的表現與穩健性。

### Method

- **要解決的問題**：既有 action-conditioned world model 大多直接以數值動作向量條件化生成模型，此範式存在兩個關鍵限制：數值動作向量缺乏顯式空間對齊，難以精確建模複雜機器人運動的細粒度互動細節；且低維動作條件化將具身運動與環境動態變化糾纏在一起，迫使模型過度關注與互動無關的場景細節（背景、光照、物件擺放等），導致模型對未見場景的泛化能力不佳、容易發生場景過擬合。

- **Main method**：GeniWorld 的核心設計是「將數值動作轉為視覺動作」（From Numerical to Visual Actions）：針對目標機器人系統，先以具身專屬的運動學模型將數值動作序列轉換為稠密的機器人運動序列（透過 URDF-based 渲染呈現機器人本體運動的視覺化表示），再以此視覺動作作為條件輸入。建立於預訓練影片生成模型之上，GeniWorld 將視覺動作與場景觀測編碼為空間對齊的潛在表示，並串接進入以因果注意力（causal attention）建構的自迴歸模型，確保未來預測嚴格依賴當前機器人動作與歷史狀態（Causal Modeling）。訓練目標採用 flow matching，讓因果 DiT（causal diffusion transformer）根據視覺動作與雜訊影片潛在表示預測未來影片。推論階段透過 KV caching 維持歷史脈絡，同時保持高品質影片生成與閉環互動能力（Efficient Closed-Loop Interaction）；操作者可將遠端操作硬體與 URDF-based 機器人運動學串接，透過 Motion Rendering 將動作即時轉為視覺動作條件，讓 world model 即時生成對應視覺回饋，達成與人類操作者的互動迴圈。

- **和以往方式的差異**：既有 action-conditioned world model（如 Ctrl-World、IRASim、EnerVerse-AC）多半直接以數值動作向量或投影後的末端執行器姿態/骨架動作作為條件，本文的消融實驗顯示這些替代表示法在場景偏移（clean-to-random）下皆出現嚴重品質衰退（如 IRASim 的 FID/FVD 大幅上升），且骨架式控制常產生物理上不合理的互動（如無接觸抓取）。GeniWorld 首次系統性地將「機器人視覺動作」本身（而非數值向量或抽象姿態表示）作為條件訊號注入影片生成骨幹，透過空間對齊的方式明確解耦具身運動學與環境動態，這是與既有數值/抽象動作條件化範式明確區隔的方法論創新，而非既有技巧的小幅組合。

- **關鍵方法圖**：見下方嵌入圖片——Figure 1 展示 GeniWorld 整體概覽：以視覺動作條件化的自迴歸機器人 world model，支援與人類操作者及機器人 policy 的閉環互動，即使僅在有限場景示範上訓練仍能泛化至分布外場景；Figure 2（方法架構圖）展示如何將機器人動作透過 URDF 渲染轉為視覺動作、編碼為潛在表示並與雜訊影片潛在表示串接，輸入因果 DiT 以 flow matching 預測未來影片。

![Figure]({{ site.baseurl }}/assets/images/2608.06332_overview.png)

_Figure 1: GeniWorld 整體概覽——以視覺動作條件化的自迴歸 world model，支援與人類操作者及機器人 policy 的閉環互動_

![Figure]({{ site.baseurl }}/assets/images/2608.06332_method.png)

_Figure 2: GeniWorld 方法架構圖——機器人動作經 URDF 渲染轉為視覺動作、編碼後與雜訊影片潛在表示串接，輸入因果 DiT 預測未來影片_

### Result

- **主要增強部分**：在基於 RoboTwin2.0 建立的 Clean-to-Clean（分布內）與 Clean-to-Random（零樣本分布外泛化）兩種評測設定下（50 項任務、2,250 訓練 episode、250 測試 episode），GeniWorld 在 PSNR、SSIM、LPIPS、FID、FVD、EWMScore 六項指標上全面優於 Ctrl-World、IRASim、EnerVerse-AC 等基線。在場景分布偏移下，IRASim 等既有方法出現嚴重品質衰退（FID/FVD 分別惡化至 174.52 與 191.26），而 GeniWorld 維持極低的 FID（13.08）與 FVD（20.15）。效率面，視覺動作條件化在推論取樣步數從 50 降至 10 或 5 步時，品質幾乎不衰退（FVD 僅劣化約 2%），遠優於數值動作條件化基線（FVD 劣化約 22%），實現約 10 倍推論加速；結合遠端操作硬體與 URDF 運動學，系統在 NVIDIA H20 GPU 上以 5 個取樣步驟達到約 8Hz 互動推論速率。下游應用上，GeniWorld 作為 policy 評估器時，其模擬中的 policy 成功率與真實世界表現呈正相關；資料生成實驗顯示，僅用 25 筆真實示範搭配 GeniWorld 合成的空間隨機化與多樣場景變化資料，可將分布外任務成功率大幅提升（如空間重排任務成功率從 37.5% 提升至 62.5%，干擾物任務從 38.8% 提升至 63.8%）。

- **結果是否公正**：論文在標準化的 RoboTwin2.0 benchmark 上與三個具代表性的既有 action-conditioned world model 基線比較，並輔以四種動作條件化設計（數值動作、末端執行器姿態、骨架動作、視覺動作）的系統性消融實驗拆解增益來源，同時在真實機器人平台上驗證 policy 評估與資料生成的下游應用，具備合理的實驗嚴謹度。惟目前全部評測皆由作者團隊自行執行，且真實世界任務數量（四項）相對有限，尚待更廣泛的第三方獨立驗證。

### Limitation

- **已知 limitation**：論文本身在正文中未設獨立的 Limitation 章節，但從方法設計與實驗範圍可推知：GeniWorld 依賴具身專屬的 URDF 運動學模型才能將數值動作轉為視覺動作，這對每個新具身都需要對應的運動學建模與渲染管線，增加跨具身部署的工程成本；此外，模型仍建立於預訓練影片生成骨幹之上，其生成品質與物理合理性上限仍受限於底層影片模型本身的先驗知識。

- **從 result 來看的弱項**：真實世界驗證僅涵蓋四項操作任務與有限的具身平台，跨任務類型（如更複雜的多階段長 horizon 任務）與跨具身（如人形機器人、雙臂協同）的泛化能力尚未見充分驗證；資料生成實驗中 25 筆示範搭配合成資料的設定雖展示了顯著提升，但合成資料規模（每任務 130 筆）相對於機器人基礎模型常見的大規模預訓練資料仍屬小規模驗證，其在更大規模資料場景下的邊際效益尚待觀察。

### Related work

- 本文與本頁「Robot-Specific Action-Conditioned World Models」主題分類下已收錄的 Ctrl-World（arXiv:2510.10125，ICLR 2026）、τ0-WM（arXiv:2606.01027）等論文同屬「以 world model 支援機器人 policy 想像式 rollout 或評估」的研究脈絡，但 GeniWorld 的「視覺動作條件化」設計與既有直接數值動作條件化方法形成明確方法論對照，論文中的消融實驗也直接以 Ctrl-World、IRASim、EnerVerse-AC 作為基線比較對象。
- 判斷值得 survey 的程度：中高。GeniWorld 提出的「視覺動作作為條件訊號」設計思路具跨架構遷移潛力，且同時驗證了 world model 作為 policy 評估器與資料生成引擎兩種下游應用，是 action-conditioned world model 方法論演進中值得持續追蹤的方向，尤其其「解耦具身運動學與環境動態」的設計理念可能影響後續同類研究的條件化策略選擇。

### Conclusion

- **綜合評價**：GeniWorld 準確指出既有 action-conditioned world model 依賴數值動作向量條件化所導致的空間對齊缺失與場景過擬合問題，並以「視覺動作」這一直觀但此前未被系統性驗證的條件化設計作為解方，在生成品質、零樣本分布外泛化、推論效率、以及下游 policy 評估與資料生成應用等多個面向均取得扎實驗證，是一篇方法論簡潔且工程實用性強的機器人 world model 論文。

- **與其他重要文章的關係**：GeniWorld 與本頁「Robot-Specific Action-Conditioned World Models」主題下的 Ctrl-World、τ0-WM、Pelican-Sim 1.0 等論文共享「以 world model 支援機器人 policy 訓練與評估」的核心關注點，但更聚焦於動作條件化表示本身的設計；也與 VLA Papers 頁面「World Models Integration」主題形成跨頁呼應。ROCm/AMD 在此領域尚待補強之處：GeniWorld 的因果 DiT 訓練與 KV caching 加速推論皆以 NVIDIA GPU（含實驗中使用的 H20）作為預設硬體環境，尚未見任何針對 ROCm 的影片擴散模型 KV caching 或流匹配（flow matching）推論加速的效能驗證；由於 GeniWorld 展示了僅需 5 個取樣步驟即可達到約 8Hz 的即時互動速率，這類「輕量取樣步數 + KV caching」的高效推論架構若能在 ROCm 平台上驗證訓練與推論效能，將是 AMD 切入機器人 world model 基礎設施市場的具體技術驗證切入點。
