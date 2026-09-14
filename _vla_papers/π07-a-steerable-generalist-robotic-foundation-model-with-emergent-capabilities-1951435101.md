---
layout: paper
title: "π0.7: a Steerable Generalist Robotic Foundation Model with Emergent Capabilities"
section: vla
page_id: "1951435101"
permalink: /Physical-AI-Papers-Survey/vla/π07-a-steerable-generalist-robotic-foundation-model-with-emergent-capabilities-1951435101/
---

### Abstract

π0.7 是 Physical Intelligence 提出的第三代通用機器人基礎模型，核心訴求是「可組合泛化」（compositional generalization）：讓一個模型能把在不同情境下學到的技能重新拼接，去解決訓練時從未見過的任務組合。方法上採用「多樣情境條件」（diverse context conditioning）訓練範式——模型的 prompt 不只包含語言指令，還包含描述資料品質/策略的 episode metadata，以及次目標圖片等多模態訊號，讓同一個模型能同時吃進示範資料、次優的自主收集資料（含失敗案例），以及非機器人來源的資料。架構為 5B 參數 VLA：4B VLM backbone + MEM 風格的影片歷史編碼器 + 860M 參數 action expert；執行時由同架構的高階語意策略產生語言指令，並由基於 BAGEL 影像生成模型的輕量 world model 產生次目標圖片。實驗顯示 π0.7 能在未見過的廚房環境中完成多階段任務、零樣本跨具身操作（如未見過摺衣服任務也能完成），並在操作濃縮咖啡機等高難度任務上，僅靠開箱即用表現就逼近專門用 RL 微調過的模型。最驚人的案例是 air fryer 任務：僅靠訓練中兩段零碎相關資料，配合半小時的自然語言教練式提示調整，成功率從約 5% 提升到約 95%。論文誠實承認一項方法論限制：在如此大規模、多樣化的資料集上，很難嚴格界定任務究竟是「已見過」還是「未見過」，因為相關技能很可能已零散地存在於資料集其他地方。

### Method

要解決的問題：現有 VLA/機器人基礎模型雖然規模與能力持續提升，但「可組合泛化」——把已學會的技能重新組合去完成全新任務——始終難以實現，這被作者視為通用具身智能的核心瓶頸。

Main method：以「多樣情境條件」訓練為核心，把 prompt 從單純語言指令擴展為多模態上下文：語言指令 + episode metadata（資料品質、策略描述）+ 次目標圖片等，使模型能精細地被「引導」（steer）用不同策略完成同一任務，並藉此吃下極度異質的資料來源（優質示範、次優/失敗的自主資料、非機器人資料）。架構上是 5B 參數 VLA：4B VLM backbone 負責感知與語言理解，MEM 風格影片歷史編碼器處理時序上下文，860M 參數的 action expert 負責動作輸出；推論時搭配同架構的高階語意策略生成語言指令，以及基於 BAGEL 影像生成模型的輕量 world model 產生次目標圖片，形成「高階語意規劃 + world-model 想像次目標 + 低階動作執行」的分工。

和以往方式的差異：相較於 π0 / π0.5 等前代僅以語言指令 + 影像作為條件，π0.7 額外引入「策略/品質 metadata」與「次目標圖片」作為條件訊號，讓同一份大規模異質資料（含次優與失敗軌跡）都能被有效利用，而不需要事先篩除低品質資料；同時透過人類「教練式」自然語言提示在測試時即時調整策略（如 air fryer 案例），這種測試時可調控性是先前 VLA 較少強調的能力。

幾張重要的論文方法截圖：Fig. 1（總覽圖，展示 π0.7 的多樣情境條件框架與整體能力）、Fig. 2（架構總覽圖，展示 4B VLM + MEM 影片編碼器 + 860M action expert 的模型結構，以及高階語意策略與 BAGEL-based world model 如何在推論時協同運作）。

![Figure](/Physical-AI-Papers-Survey/assets/images/1951435101_pi07_fig1.png) 

![Figure](/Physical-AI-Papers-Survey/assets/images/1951435101_pi07_arch.png) 

### Result

Result 結果如何，主要增強了哪些部分：π0.7 在多階段廚房任務、跨具身摺衣（未見過的任務）、操作濃縮咖啡機等挑戰性任務上表現出色，開箱即用即可達到接近專門 RL 微調模型的水準。最具代表性的 air fryer 案例：訓練資料中僅有兩段零碎相關示範，透過半小時的人類自然語言教練式提示調整，成功率從約 5% 提升到約 95%，展現極強的組合式泛化與可引導性。

Result 是否公正，其他論文提出的結果有沒有和這篇論文 result 不符：論文本身在方法論上相當坦誠，明確指出「大規模多樣資料集下難以嚴格界定任務是否真正『未見過』」這個限制，並未過度誇大泛化能力的來源。目前未見到其他論文對 π0.7 具體數字提出直接反駁或矛盾證據，但由於 Physical Intelligence 是 π 系列的原始開發者，其自我報告的成功率评测（尤其是「教練式提示」這種帶有人類即時介入的實驗設計）仍需第三方在獨立環境中復現，才能完全排除評測設計偏誤的可能。

### Limitation

有沒有已知的 limitation：作者明確承認，在極大規模、多樣化的資料集上，「這個任務到底算不算模型真正沒見過」在實務上很難嚴格定義——因為相關技能或行為片段可能已經以不同標籤、或作為其他任務的一部分，零散地存在於龐大資料集中的其他地方。

從 result 來看 limitation 和弱項是甚麼：air fryer 案例的成功需要人類即時「教練式」語言提示介入，這意味著純粹的零樣本泛化能力可能不如展示案例看起來那麼強，實際部署時仍可能需要人類在場微調提示才能達到高成功率；此外論文評測場景多由 Physical Intelligence 自行設計與執行，缺乏獨立第三方復現的驗證。

### Related work

arXiv 上有沒有更新的 related work：與本頁已收錄的 DreamZero（World Action Models are Zero-shot Policies, arXiv:2602.15922）、以及 VLA Papers 頁面中的 τ0-VLA（arXiv:2608.16885）都屬於「用 world model / 次目標想像輔助高階決策」這一路線的最新發展，可互相對照比較 VLA 路線 vs. World Action Model 路線在泛化能力上的差異。另外 VLA Papers 頁面已收錄的 MemoryVLA++（arXiv:2606.09827）在「記憶 + 想像」的設計上與 π0.7 的 MEM 影片編碼器+ BAGEL world model 設計有相近的問題意識，值得對照研讀。

判斷 related work 值得 survey 的程度：值得。DreamZero 代表了與 π0.7 完全不同的技術路線（World Action Model，以影片擴散骨幹統一動作與影片預測），兩者在 2026 年構成了「VLA vs. WAM」的核心路線之爭，對 AMD/ROCm 評估自身在具身智能領域該投入哪條技術路線具有直接參考價值。

### Conclusion

給這篇文章綜合評價，值不值得參考：非常值得參考。π0.7 出自 Physical Intelligence（RSS 2025 π0 的原創團隊），是目前 VLA 路線最具代表性的旗艦級研究之一，其「多樣情境條件」訓練範式與測試時可引導性，為解決 VLA 長期缺乏可組合泛化能力的問題提供了具體且可驗證的技術路徑，是 2026 年具身智能領域繞不開的重要參考點。

做出跟其他重要文章的關係相依圖，並判斷 ROCm/AMD 在此領域上尚待補強的部分：π0.7 上游承接 π0（arXiv:2410.24164，flow-matching 連續動作）與 π0.5，並與同期 DreamZero（World Action Model 路線，arXiv:2602.15922）形成路線對照；其 BAGEL-based 次目標想像設計又與 VLA Papers 頁面的 MemoryVLA++、World Model Papers 頁面的 τ0-WM 等「world model 輔助決策」研究有方法論上的交集。就 ROCm/AMD 現況而言，π0.7 這類需要「4B VLM + 860M action expert + 額外 world model」多模組協同推論的系統，對邊緣/機器人端即時推論的軟體堆疊（低延遲多模型調度、KV-cache 管理、跨模組記憶體共享）要求極高，而目前 ROCm 生態在這類異質多模型即時協同推論（尤其是結合 diffusion-based world model 的閉環控制）上的參考實作與效能調優案例仍明顯少於 CUDA 生態（如 NVIDIA Cosmos/GR00T 系列已有成熟的部署範例），這是 AMD 若要切入具身智能/機器人市場需要優先補強的一塊。