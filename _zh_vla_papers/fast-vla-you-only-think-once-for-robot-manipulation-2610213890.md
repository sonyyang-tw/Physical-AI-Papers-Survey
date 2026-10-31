---
layout: paper
title: "Fast-VLA: You Only Think Once for Robot Manipulation"
section: vla
page_id: "2610213890"
permalink: /zh/vla/fast-vla-you-only-think-once-for-robot-manipulation-2610213890/
---

### Abstract

VLA policy 普遍將數十億參數規模的 VLM 置於控制閉環之中，每當預測新的 action chunk 時都要重新計算一次任務情境，然而任務理解的變化速度遠慢於機器人狀態本身的變化速度。本論文提出 Fast-VLA，於每個 episode 開始時僅呼叫一次凍結的 4B VLM，將指令與初始多視角畫面編碼為固定的、逐層的 key-value 任務記憶（task memory）；執行期間，一個輕量的線上 actor 將可學習的時間索引與手臂索引查詢（query）與目前的視覺/本體感覺回饋融合，從固定記憶中擷取任務情境並預測 action chunk，完全不需重新運行基礎模型。Fast-VLA 在 RoboTwin 2.0 Clean 與 Randomized 上分別達到 92.46% 與 92.40% 成功率，在 LIBERO 與 LIBERO-Plus 上分別達到 95.95% 與 79.11%；相較於同硬體上的三個持續條件化基線，RoboTwin 攤銷後的 policy 推論時間降低 10.9–17.1 倍，post-prefill 線上常駐記憶體僅需 1.22 GiB。論文於 2026 年 10 月 15 日發佈於 arXiv，作者團隊來自華為新加坡研究中心（Huawei Singapore Research Center），屬產業實驗室出品的 VLA 推論效率代表作。

### Method

- **要解決的問題**：VLA policy 常見設計是將多億參數規模的 VLM backbone 直接置於閉環控制之中，每預測一次新的 action chunk 就重新運行一次完整前向傳播，即便任務理解（instruction grounding、場景語意）在整個 episode 中幾乎不變。這種「持續重新思考」的設計造成嚴重的推論瓶頸：高延遲導致閉環控制頻率受限，也限制了大型 VLM 在真實機器人上的實用部署密度。

- **Main method**：Fast-VLA 的核心洞察是將「任務理解」與「逐步控制」解耦。在每個 episode 開始時，一個凍結的 4B VLM 僅運行一次，將指令與初始多視角畫面編碼為固定的、逐層的 key-value（KV）任務記憶，此後整個 episode 不再重新呼叫該 VLM。執行期間，一個輕量的線上 actor 以可學習的、依時間與手臂索引的 query，結合當下的視覺與本體感覺回饋構成 action query，這些 query 從固定的 KV 任務記憶中擷取任務情境，據此預測 action chunk，全程不需重跑基礎模型。

- **和以往方式的差異**：既有 VLA 設計（包括多數持續條件化基線）將 VLM 視為閉環控制的一部分，每個控制步驟都重新編碼情境，造成計算冗餘與延遲瓶頸；Fast-VLA 則明確區分「情境建立」（episode 開始時一次性完成）與「閉環控制」（僅由輕量 actor 負責、高頻運行），讓大型 VLM 的語意理解能力與控制迴圈的響應性解耦。任務記憶替換實驗（task-memory swap）證實 actor 確實依賴與當前 episode 相符的任務記憶，驗證此一次性情境建立策略的有效性，而非僅是性能與正確性之間的妥協。

- **關鍵方法圖**：見下方嵌入圖片——第一張圖展示 Fast-VLA 在 RoboTwin 2.0 上成功率與攤銷推論延遲的權衡關係，氣泡大小代表線上常駐記憶體、顏色代表方法家族；第二張圖展示 Fast-VLA 的記憶條件化線上控制架構，呈現凍結 VLM 如何於 episode 開始時建構固定 KV 任務記憶、線上 actor 如何逐步擷取情境並預測動作。

![Figure]({{ site.baseurl }}/assets/images/2610.21389_fastvla_teaser.png)

_Figure 1: Fast-VLA 每個 episode 僅思考一次——RoboTwin 2.0 上成功率 vs. 攤銷推論延遲的權衡關係，氣泡大小代表線上常駐記憶體_

![Figure]({{ site.baseurl }}/assets/images/2610.21389_fastvla_arch.png)

_Figure 2: Fast-VLA 記憶條件化線上控制架構——凍結 VLM 建構固定 KV 任務記憶，輕量線上 actor 擷取情境並預測 action chunk_

### Result

- **主要增強部分**：Fast-VLA 在 RoboTwin 2.0 Clean 與 Randomized 設定下分別達到 92.46% 與 92.40% 成功率；在標準 LIBERO 與 LIBERO-Plus 評測上分別達到 95.95% 與 79.11% 成功率。相較於同一硬體上的三個持續條件化基線，Fast-VLA 將 RoboTwin 攤銷後的 policy 推論時間降低 10.9 至 17.1 倍，且 post-prefill 階段的線上常駐記憶體僅需 1.22 GiB，大幅低於持續重新運行 VLM 的基線。任務記憶替換實驗（在不額外訓練的前提下交換不同 episode 的任務記憶）進一步證實線上 actor 確實依賴與當前 episode 相符的任務記憶，驗證了固定記憶機制的有效性而非偶然巧合。

- **結果是否公正**：論文在 RoboTwin 2.0（含 Clean 與 Randomized 兩種設定）與 LIBERO/LIBERO-Plus 兩套公開 benchmark 上皆進行了完整評測，並與三個持續條件化基線在同一硬體上直接比較推論延遲與記憶體開銷，同時提供了任務記憶替換、記憶建構方式、線上輸入組合、任務記憶刷新頻率、記憶編碼器選擇等多項消融實驗（Table 4–9），對解耦設計的各個環節逐一驗證，顯示作者對結果穩健度有充分交代，而非僅報告單一端到端數字。

### Limitation

- **已知 limitation**：論文並未在正文明確列出限制章節，但從方法設計可推論：Fast-VLA 假設任務理解在整個 episode 中保持穩定，若任務目標在執行過程中發生根本性變化（例如中途需要重新理解指令或應對意外的場景語意轉變），固定的 KV 任務記憶可能無法反映新的情境，需要依賴重新觸發 VLM 編碼或額外機制處理。

- **從 result 來看的弱項**：真實世界驗證未見於本篇摘要與結果呈現中，評測集中於 RoboTwin 2.0 模擬 benchmark 與 LIBERO/LIBERO-Plus，尚未如同本頁其他效率類論文（如 IMLE-VLA）一樣提供真實機械臂上的延遲與任務成功率驗證，真實硬體部署下的延遲增益與穩健性仍待進一步確認。

### Related work

- Fast-VLA 與本頁「Efficiency」主題下已收錄的多篇論文（如 IMLE-VLA、EcoVLA、VLA-Adapter）同屬「讓 VLA 可實際部署」這一方向，但切入點明確不同：IMLE-VLA 聚焦於以單步 cIMLE 動作頭取代迭代式 diffusion/flow-matching 動作頭，EcoVLA 聚焦於 device-edge 協同推論的能源最佳化，而 Fast-VLA 的獨特貢獻在於解耦「VLM 情境建立」與「閉環控制」兩個時間尺度，是效率議題上與既有「壓縮動作頭」或「壓縮模型本身」路線互補的第三種思路——透過減少 VLM 呼叫頻率而非縮小模型規模或動作頭複雜度來換取推論效率。
- 判斷值得 survey 的程度：高。Fast-VLA 出自華為新加坡研究中心，在 RoboTwin 2.0 與 LIBERO/LIBERO-Plus 兩套業界常用公開 benchmark 上都取得具競爭力的成功率，同時推論延遲降低超過一個數量級，消融實驗設計完整（涵蓋記憶建構方式、線上輸入、刷新頻率、編碼器選擇等多個面向），對於理解「VLM 推論頻率 vs. 控制迴圈響應性」這一 VLA 部署核心權衡具有高度參考價值。

### Conclusion

- **綜合評價**：Fast-VLA 針對 VLA 部署中「任務理解變化緩慢、但控制迴圈需要高頻響應」這一結構性落差，提出了簡潔且經過充分驗證的解耦設計——將大型 VLM 的語意理解能力收斂為一次性的固定任務記憶，交由輕量 actor 負責高頻控制。其核心創新不在於壓縮模型本身，而在於重新設計「何時」呼叫大型模型，這一設計思路與本頁同主題下聚焦「壓縮動作頭」或「壓縮模型規模」的論文形成明確區隔，並以超過一個數量級的推論加速與具競爭力的成功率數字證明其實用價值。

- **與其他重要文章的關係**：Fast-VLA 可與本頁「Architecture Paradigms」主題下聚焦動作生成機制效率的論文（如 SnapFlow、IMLE-VLA）互補對照——後者關注「動作如何被更快地解碼」，Fast-VLA 則關注「情境理解何時需要被重新計算」，兩者分屬 VLA 推論管線中不同環節的效率最佳化。ROCm/AMD 在此領域尚待補強之處：論文的訓練與推論管線雖未在正文明確揭露具體 GPU 型號，但其延遲與記憶體開銷的評測方法論（Table 11 所述協定）高度適用於跨硬體平台比較；隨著「KV 任務記憶快取」這類解耦策略逐漸成為業界降低 VLA 部署成本的標準手法，若 AMD 欲在機器人 VLA 推論基礎設施市場站穩腳步，驗證此類長期 KV-cache 常駐、低頻 VLM 呼叫搭配高頻輕量 actor 的混合推論模式在 ROCm 軟體棧上的相容性與效能表現，將是具體且有產業急迫性的生態系拓展方向。
