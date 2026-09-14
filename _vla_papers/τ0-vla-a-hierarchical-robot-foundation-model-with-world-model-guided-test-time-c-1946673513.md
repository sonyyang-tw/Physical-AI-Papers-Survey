---
layout: paper
title: "τ0-VLA: a Hierarchical Robot Foundation Model with World-Model-Guided Test-Time Computation"
section: vla
page_id: "1946673513"
permalink: /vla/τ0-vla-a-hierarchical-robot-foundation-model-with-world-model-guided-test-time-c-1946673513/
---

### Abstract

-

長 horizon 機器人操作任務需要機器人同時「可靠執行單一技能」和「在延展的任務序列上做出連貫的決策」。多數現有的階層式 (hierarchical) VLA 模型對每個高階決策僅用單次前向傳播 (single forward pass) 完成，沒有機制可以在困難或關鍵的決策點上分配額外運算資源。本文提出 τ0-VLA，一個階層式機器人基礎模型，將高階子任務 (subtask) 生成重新定義為透過 world-model 引導的測試時運算 (test-time computation, TTC) 的可擴展推論問題。在每個推論步驟中，高階策略利用執行記憶 (execution memory) 生成子任務，並在需要時對多個候選方案進行搜尋後才做出最終決策；低階策略則負責在多種機器人具身 (embodiment) 上執行生成的子任務。整個系統在 40,115 小時的異質真實世界資料上以多模態共同訓練 (multimodal co-training) 完成訓練。無論在同分布或分布偏移 (distribution-shifted) 的情境下，投入額外測試時運算皆能大幅提升「下一個子任務」預測的準確率，且這些準確率的提升確實能轉化為長 horizon 真實機器人操作任務更高的閉環 (closed-loop) 成功率。

![Figure](/assets/images/1946673513_teaser2.png) ![Figure](/assets/images/1946673513_framework2.png) 

### Method

-

要解決的問題：長 horizon 機器人操作（例如整理房間、備料、炒番茄炒蛋、做奶茶）需要橫跨導航、物體搜尋、操作、狀態追蹤與錯誤恢復等多階段流程；傳統階層式 VLA 的高階策略每次只做一次前向推論就承諾一個子任務，無法針對「困難或影響深遠」的決策分配更多計算資源，也容易在遮蔽性低（例如加鹽這種視覺變化很小的動作）的狀態下產生重複或遺漏動作。

-

main method：τ0-VLA 由「高階策略 (high-level policy) μ」與「低階策略 (low-level policy)」組成。高階策略內部包含四個子模型：(1) proposal model P，依據當前多視角觀測、任務指令、既有執行記憶與前一步生成的子任務，更新記憶並產生一個直接候選子任務；同一次前向傳播中，token 置信度會驅動一個 adaptive router 決定要走「快速路徑」(g=0) 還是啟動 TTC (g=1)；(2) world model W 與 (3) value model V：在 TTC 路徑上，proposal model 針對每個保留分支生成 N 個候選子任務，world model 依據頭部相機影像與候選子任務預測終端影像，value model 則依任務指令、候選方案與預測影像給出品質分數；(4) 透過 beam search 全域保留分數最高的 B 個分支並遞迴展開至深度 D，最終由 reflective model F 依保留分支摘要生成最終子任務（不侷限於已保留的候選集合）。低階策略則以生成的子任務、多視角觀測、本體感覺狀態與文字控制中繼資料為條件，透過一個視覺語言 backbone 搭配 Mixture-of-Transformers (MoT) 動作專家，以條件式 flow matching 從雜訊動作片段生成最終動作片段。

-

和以往方式的差異：與大多數「單次前向傳播即承諾子任務」的階層式 VLA（例如標準的高階 planner + 低階 controller 架構）不同，τ0-VLA 把高階子任務生成本身視為一個「可依難度動態擴展運算量」的推論問題，並用 world model 對候選子任務的「視覺結果」做預測與評分，而非僅依賴語言層面的推理；論文也特別指出，它與其他「用 world model 指導『已選定子任務』如何被執行」的方法不同——τ0-VLA 是用 world model 來輔助「選擇該執行哪一個子任務」。

-

（已插入論文概論圖 Fig.1 於本節前方，以及 Fig.2 系統架構圖）

### Result

-

在四項長 horizon 真實機器人任務（Clean Room / Prepare Ingredients / Tomato and Egg Stir Fry / Make Milk Tea，各 10 次獨立真實機器人試驗）中，τ0-VLA（Hierarchical System, Plan Once）取得平均成功率 (SR) 45.00% 與平均 Progress 87.85%，優於同設定下的 GR00T N1.7（SR 2.50%, Progress 45.29%）、LingBot-VLA（SR 0.00%, Progress 44.43%）與 π0.5（SR 22.50%, Progress 73.05%），也優於未使用階層記憶、僅以完整指令直接執行的 τ0-VLA 單體版本（SR 27.50%, Progress 80.10%）。分項來看：Clean Room 受益於顯式執行記憶（跨房間轉換時仍能保留進度）；Prepare Ingredients 的失敗多集中於雞蛋撿取/打蛋/攪拌等前置步驟，記錄已完成階段特別有幫助；Tomato and Egg Stir Fry 的瓶頸在於加鹽這類視覺變化極小的步驟，缺乏顯式進度記錄的策略容易重複加鹽或漏加，階層系統透過顯式記錄調味進度解決此問題；Make Milk Tea 則是兩個 τ0-VLA 版本都已表現不錯的情境。

-

在測試時運算 (TTC) 實驗中（Make Milk Tea / Book Organization / Clean Room），閉環真實機器人評測顯示 TTC 相較 Plan Once 基準線全面提升：Make Milk Tea SR 由 5/10 提升至 7/10（Progress 91.92%→95.38%）、Book Organization SR 由 6/10 提升至 9/10（Progress 66.67%→93.33%）、Clean Room SR 由 5/10 提升至 7/10（Progress 94.80%→97.60%）。開環實驗也顯示，隨著投入的運算成本增加，下一步子任務預測準確率呈飽和曲線上升，且皆優於 Plan Once 基準。

-

result 是否公正：對照組（GR00T N1.7、LingBot-VLA、π0.5）皆為近期公開的重要 VLA/機器人基礎模型，比較設定（相同的觀測/動作介面、固定低階策略）具一定控制變因的嚴謹度；但所有結果皆為作者自行以真實機器人小樣本（每任務 10 次試驗）進行的評測，樣本量偏小，且評測任務與資料由作者自建，尚未看到獨立第三方復現結果，摘要與正文亦未提及與其他機構（如 NVIDIA、Physical Intelligence）近期模型的橫向比較是否存在爭議。

### Limitation

-

論文正文與摘要並未明確列出獨立的「Limitation」章節；以下限制根據 Method/Result 內容推論，屬於「摘要/全文未明確承認、需要查證全文附錄」的合理推測：(1) TTC 機制引入額外的世界模型推論與 beam search，增加推論延遲與算力成本，是否能滿足即時控制的頻率需求，論文未在此文本段落中充分討論；(2) 真實機器人評測樣本量小（每任務僅 10 次試驗），統計顯著性有限；(3) world model 對「終端視覺結果」的預測品質直接決定 value model 評分準確度，若 world model 本身存在幻覺或分布外預測誤差，可能反而誤導高階決策（此為此類 world-model-guided 方法的一般性風險，全文是否有針對性分析需要查證原文附錄 C 部分）。

-

從 result 來看，弱項可能在於：Prepare Ingredients 任務的 SR 仍偏低（4/10），顯示對於需要精細操作（雞蛋撿取/打蛋）的前置步驟，即使有階層式記憶機制仍難以完全解決精細操作失敗導致的連鎖影響。

### Related work

-

論文將自身定位於三條相關研究主線：(1) Vision-Language-Action Models（如 π0、π0.5、RT-H 等）；(2) Hierarchical Robot Policies（高階規劃+低階控制的階層式系統）；(3) World Models and Test-Time Computation。arXiv 上已有多篇 2026 年新作討論類似方向，例如同樣使用 world model 輔助 VLA 決策的 "World Action Models: The Next Frontier in Embodied AI"（arXiv:2605.12090，已收錄於本頁）與 "In-Context World Modeling for Robotic Control"（arXiv:2606.26025，已收錄於本頁），以及同為階層式推理方向的 "What Matters in Orchestrating Robot Policies"（arXiv:2606.10267，已收錄於本頁）。

-

判斷 related work 值得 survey 的程度：τ0-VLA 的「world-model 引導測試時運算搜尋子任務」與既有的「world model 輔助動作生成」路線（本頁主題分類 7）有明確區隔，是本頁目前收錄論文中少數將 test-time compute scaling 概念系統性應用於階層式 VLA 高階決策的作品，值得作為主題分類 2（Hierarchy）與 7（World Models Integration）的交叉參考論文持續追蹤。

### Conclusion

-

綜合評價：τ0-VLA 出自 Agibot Finch（與 Shanghai Innovation Institute、香港中文大學合作），符合本次選文標準中的「科技大廠/知名實驗室出品」（Agibot 為知名具身智能新創）與「方法論真正創新」（將 test-time compute scaling 引入階層式 VLA 的高階子任務生成，並用 world model 預測視覺結果作為候選評分依據，是一個相對新穎的組合，而非既有技巧的小幅疊加）。40,115 小時的真實世界訓練資料規模也顯示出工業級的資源投入。整體而言值得參考，尤其對於長 horizon、多階段、有隱性狀態追蹤需求（如烹飪類任務）的機器人應用場景有直接參考價值。

-

與其他重要文章的關係：τ0-VLA 座落於「Hierarchy: High-Level Planning/Reasoning vs Low-Level Control」（主題分類2）與「World Models Integration」（主題分類7）的交會處，可與 What Matters in Orchestrating Robot Policies（分類2，options 框架的系統性研究）、World Action Models（分類7，WAM 分類定義）、DeepThinkVLA（分類2，latent CoT 推理是否驅動決策）形成比較群組；亦可與基礎模型 GR00T N1、π0（本頁「基礎/參考模型」）比較低階策略設計。ROCm/AMD 在此領域尚待補強的部分：τ0-VLA 的 MoT 動作專家與 flow matching 低階策略、以及高階 world model + value model 的多模型並行推論架構，對硬體側的「多模型併發排程」與「flow-matching 去噪迭代的低延遲推論」皆有較高要求；目前公開資料未提及其推論後端是否使用 ROCm 或特定加速庫，這是可以進一步向作者/社群查證、並評估 AMD GPU 平台在此類多子模型階層式 TTC 推論管線上效能定位的方向。