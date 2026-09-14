---
layout: paper
title: "World Action Models are Zero-shot Policies (DreamZero)"
section: wm
page_id: "1951337490"
permalink: /Physical-AI-Papers-Survey/wm/world-action-models-are-zero-shot-policies-dreamzero-1951337490/
---

### Abstract

DreamZero 是 NVIDIA 主導（作者含 Linxi "Jim" Fan、Jan Kautz、Yuke Zhu 等）提出的 World Action Model（WAM），核心主張是：現有 state-of-the-art VLA 模型雖擅長語意層面的泛化，卻難以泛化到新環境中「未見過的物理動作」。DreamZero 建立在預訓練的影片擴散骨幹（Wan2.1-I2V-14B-480P，14B 參數的 image-to-video diffusion model）之上，透過聯合建模影片與動作——把影片視為「世界如何演化」的稠密表徵——從異質機器人資料中有效學習多樣技能，而不需依賴大量重複示範。真實機器人實驗顯示，相較於 state-of-the-art VLA，DreamZero 在新任務與新環境的泛化能力上取得超過 2 倍的提升；透過系統與模型層級的優化，團隊成功讓一個 14B 自迴歸影片擴散模型達到 7Hz 的即時閉環控制。論文並展示兩種跨具身遷移能力：僅用 10-20 分鐘的其他機器人或人類影片示範，就能在未見任務上取得超過 42% 的相對效能提升；更令人意外的是，DreamZero 僅需 30 分鐘的新機器人（YAM）play data 就能完成少樣本具身適應，同時保留零樣本泛化能力。在 2026 年 4 月的 RoboArena 排行榜上，DreamZero（基於 Wan 2.1-I2V-14B 的 joint-prediction WAM）拿下 1750 Elo，領先 π0.5 的 1622 與 π-FAST 的 1592，是目前 WAM 路線最具代表性的實證成果之一。

### Method

要解決的問題：現有 VLA（如 π 系列、OpenVLA 等）在語意泛化（理解新指令、新物件名稱）上表現優異，但在「新環境中的物理動作泛化」上表現不佳——換言之，模型能聽懂新任務，卻不一定能正確執行對應的物理動作序列。

Main method：不同於 VLA 把動作生成視為獨立於視覺理解的下游模組，DreamZero 讓同一個影片擴散骨幹同時對「動作」與「未來影片幀」做聯合去噪預測（joint video-action modeling），也就是把動作生成內化為影片生成過程的一部分。這使模型能直接從影片資料（包含大量非機器人動作標註的人類/其他機器人影片）中學習物理動態，而不必依賴大量重複的機器人示範資料。為了讓 14B 參數的自迴歸影片擴散模型能達到 7Hz 即時閉環控制，論文在系統層級（system-level）、實作層級（implementation-level）與模型層級（model-level，即 DreamZero-Flash）三個層次做了針對性優化。

和以往方式的差異：相較於傳統 VLA 將 VLM 理解與動作解碼視為兩個階段（甚至兩個獨立模組），DreamZero 用「video as dense world representation」的視角統一了兩者——影片預測本身就隱含了物理動態的理解，動作只是這個預測過程的一個維度。這使得跨具身遷移（cross-embodiment transfer）變得更自然：只要有影片（不論是人類、其他機器人拍攝），就能作為訓練訊號，而不需要該影片帶有與目標機器人相同的動作標註。

幾張重要的論文方法截圖：Figure 1（總覽圖，展示 DreamZero 的整體概念與泛化能力對比）、Figure 4（模型架構圖，展示 joint video-action 擴散骨幹如何處理輸入觀測、生成未來影片幀與對應動作序列）。

![Figure](/Physical-AI-Papers-Survey/assets/images/1951337490_dz_overview.png) 

![Figure](/Physical-AI-Papers-Survey/assets/images/1951337490_dz_arch.png) 

### Result

Result 結果如何，主要增強了哪些部分：DreamZero 相較 state-of-the-art VLA 在新任務/新環境泛化上取得超過 2 倍提升；透過影片示範（人類或其他機器人）的跨具身遷移，僅用 10-20 分鐘資料就能在未見任務上取得超過 42% 相對效能提升；僅用 30 分鐘 play data 即可完成向全新機器人具身（YAM）的少樣本適應。在 RoboArena 公開排行榜（2026 年 4 月）上以 1750 Elo 排名第一，明顯領先 π0.5（1622）與 π-FAST（1592）。

Result 是否公正，其他論文提出的結果有沒有和這篇論文 result 不符：RoboArena 是第三方維護的公開評測排行榜，DreamZero 在其上的排名（而非僅由作者自行報告的內部評測）具有一定的可信度與可比較性，這比純粹自我報告的成功率更具說服力。專案已開源模型權重、推論程式碼，以及在 RoboArena、PolaRiS、Genie Sim 3.0 上的評測程式碼，可供第三方復現，透明度較高。目前未見到其他論文對其 RoboArena 排名提出直接反駁。

### Limitation

有沒有已知的 limitation：論文自陳，DreamZero 在需要「次毫米級精度」的高精度操作任務（如插銷、精密組裝）上，繼承了行為克隆（behavior cloning）方法普遍存在的限制——其多樣化預訓練策略偏重「廣度」，可能underrepresent 高精度操作所需的密集示範資料。作者也引用同期研究（Kim et al., 2026）指出 WAM 路線在毫米級精度任務上可能反而具有優勢，暗示「廣泛泛化」與「精細操作」之間的取捨未必不可調和，但這在 DreamZero 本身的實驗中尚未被驗證。

從 result 來看 limitation 和弱項是甚麼：14B 參數的影片擴散模型即便經過大量系統優化才勉強達到 7Hz 閉環控制，相較於傳統輕量 VLA（可達數十 Hz），推論延遲仍是實際部署的一大瓶頸，尤其對於需要高頻反饋修正的精細操作任務可能不利。

### Related work

arXiv 上有沒有更新的 related work：與 World Model Papers 本頁已收錄的 τ0-WM（arXiv:2606.01027, AGIBOT）、VLAW（arXiv:2602.12063）同屬「video-action 聯合建模」路線，可互相比較不同團隊（NVIDIA vs. AGIBOT）在此設計思路下的實作差異。此外 VLA Papers 頁面收錄的「World Action Models: The Next Frontier in Embodied AI」（arXiv:2605.12090）明確將 DreamZero 式的 Joint WAM 與 Cascaded WAM 並列討論，可作為理解本文在整體 WAM 分類體系中定位的補充讀物；同一時期出現的 π0.7（arXiv:2604.15483, Physical Intelligence，已收錄於 VLA Papers 頁面）代表了「VLA 陣營」對同一泛化問題的另一種解法，兩篇論文構成 2026 年具身智能領域最重要的路線對照組。

判斷 related work 值得 survey 的程度：非常值得。DreamZero 與 π0.7 分別代表 WAM 與 VLA 兩大陣營在 2026 年上半年的旗艦級成果，兩者對「如何達成可泛化的具身智能」給出截然不同的答案，對照研讀能幫助釐清兩條路線各自的優劣勢與適用場景。

### Conclusion

給這篇文章綜合評價，值不值得參考：非常值得參考。DreamZero 出自 NVIDIA 大型團隊（含知名研究者 Linxi "Jim" Fan、Jan Kautz），並在第三方 RoboArena 排行榜上取得驗證過的第一名成績，是目前 World Action Model 路線最具說服力的實證研究之一，對於評估「影片擴散骨幹 + 聯合動作建模」這條技術路線的可行性極具參考價值。

做出跟其他重要文章的關係相依圖，並判斷 ROCm/AMD 在此領域上尚待補強的部分：DreamZero 建立在 Wan2.1-I2V-14B 影片擴散骨幹之上，與同屬 WAM 路線的 τ0-WM（AGIBOT）、VLAW 構成技術系譜；同時與 VLA 陣營的 π0.7、以及本頁其他 baseline（GAIA-2、V-JEPA 2 等影片世界模型）形成跨路線對照。就 ROCm/AMD 現況而言，DreamZero 這類需要把 14B 參數自迴歸影片擴散模型優化到 7Hz 即時閉環控制的工作，高度依賴針對影片擴散模型的系統級/實作級/模型級三層優化（如 KV-cache 重用、逐步去噪加速、混合精度調度等）；NVIDIA 憑藉 Cosmos 系列與自身硬體的深度協同優化，已在這類「大型影片生成模型即時機器人控制」場景建立起明顯的先發優勢，而 ROCm 生態目前在影片擴散模型的即時推論優化（尤其是自迴歸架構下的低延遲閉環控制）上仍缺乏對應的公開範例與效能基準，是 AMD 若要在 WAM 路線的具身智能競賽中佔有一席之地，需要優先建立的軟體堆疊能力。