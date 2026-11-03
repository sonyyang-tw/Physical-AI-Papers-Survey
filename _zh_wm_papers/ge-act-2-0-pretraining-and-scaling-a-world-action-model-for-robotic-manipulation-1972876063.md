---
layout: paper
title: "GE-Act 2.0: Pretraining and Scaling a World-Action Model for Robotic Manipulation"
section: wm
page_id: "1972876063"
permalink: /zh/wm/ge-act-2-0-pretraining-and-scaling-a-world-action-model-for-robotic-manipulation-1972876063/
---

### Abstract

World-Action Models (WAM) 透過預測未來狀態來引導機器人動作，使其能同時從無動作標籤的影片與有動作標籤的互動資料中學習。然而，現有大多數 WAM 都是在既有預訓練影片生成器的基礎上進行後訓練，WAM 專屬的預訓練與規模化方式本身仍未被充分探索。本文提出 Genie Envisioner Act 2.0（GE-Act 2.0），其可訓練的生成式與動作元件皆從零開始、完全在操作資料上訓練，而非繼承既有影片生成骨幹。系統結合三個模組：control-oriented autoencoder（CoAE）在激進壓縮下保留動作/指令相關資訊；single-step visual planner（SVP）以單次可微分前向傳播產生完整未來狀態；inverse dynamics model（IDM）從狀態轉移中回推動作。三者以 knowledge-aligned selective optimization（KASO）聯合訓練，此策略僅挑選被判定與已記錄動作行為一致的預測未來，過濾掉監督訊號不匹配的樣本。在 100 項任務、20 個技能群組、涵蓋未見場景/背景/光照/物件實例的零樣本（無任務專屬微調）評測中，將共訓練資料規模從 300 小時擴大到 30,000 小時，成功率從 17.1% 提升至 44.1%（G1-OP）、13.4% 提升至 31.1%（G2-90D）；儘管 G2-90D 資料佔共訓練資料不到 2%，仍提升 17.7 個百分點，顯示跨具身遷移能力。增益涵蓋 19/20 與 18/20 個技能群組，且技能特定的資料覆蓋率與零樣本分佈外（OOD）成功率高度相關（Pearson r=0.80）。同一協議下，模型在至少 90% 試驗中能正確 grounding 物件、顏色、形狀與位置指涉，並能在指令與已承諾行為或既有場景關聯衝突時仍遵循明確指令。由 AgiBot Research Team 發表技術報告，尚未見正式會議接受標記。

### Method

- **要解決的問題**：現有大多數 World-Action Models 皆繼承自預訓練影片生成器（如既有的 video diffusion 骨幹）進行後訓練，這種「借用式」路線使得 WAM 專屬的從零預訓練與資料規模化規律始終未被系統性驗證——究竟 WAM 需要多少操作資料、以何種架構才能在零樣本（無任務專屬微調）情境下達到可用的泛化能力，仍是開放問題。

- **Main method**：GE-Act 2.0 由三個從零訓練的模組組成：(1) control-oriented autoencoder（CoAE）在對觀測進行激進壓縮的同時，刻意保留與動作、指令相關的資訊，避免因壓縮而遺失決策所需訊號；(2) single-step visual planner（SVP）以單一可微分前向傳播直接生成完整的未來狀態，使視覺規劃與逆動態建模可以在互補資料上分別預訓練；(3) inverse dynamics model（IDM）從狀態轉移中回推出對應動作。三個模組透過 knowledge-aligned selective optimization（KASO）聯合訓練——此機制會篩選並僅保留被判定與實際記錄動作行為相容的預測未來，藉此降低監督訊號不匹配（mismatched supervision）帶來的訓練雜訊。評測方式為直接使用預訓練 checkpoint、不做任何逐任務微調（zero-shot），在 100 項任務、20 個技能群組、且場景/背景/光照/物件實例皆為未見過（held-out）的條件下測試。

- **和以往方式的差異**：與既有「借用預訓練影片生成器再後訓練」的 WAM 路線不同，GE-Act 2.0 的生成式與動作元件皆從零開始、完全在機器人操作資料上訓練，這使其能直接驗證「WAM 資料規模化」本身的效果，而非受限於既有影片生成骨幹的先驗偏好或架構限制。CoAE/SVP/IDM 的解耦設計，加上 KASO 選擇性監督對齊機制，是與既有級聯式（cascaded）WAM 設計或單一影片擴散骨幹聯合去噪方案明確區隔的架構創新。

- **重要方法截圖**：見下方嵌入圖片——系統架構圖展示 CoAE / SVP / IDM 三模組如何透過 KASO 聯合訓練；資料規模化曲線圖展示訓練資料時數（300 小時至 30,000 小時）與零樣本 OOD 成功率之間的關係。

![Figure]({{ site.baseurl }}/assets/images/2609.05588_geact_system.png)

_Figure: GE-Act 2.0 系統架構 — CoAE / SVP / IDM 三模組如何透過 KASO 聯合訓練_

![Figure]({{ site.baseurl }}/assets/images/2609.05588_geact_taskladder.png)

_Figure: 資料規模化曲線 — 訓練資料時數（300 小時至 30,000 小時）與零樣本 OOD 成功率之間的關係_


### Result

- **主要增強部分**：將共訓練資料規模從 300 小時擴大到 30,000 小時，G1-OP 零樣本 OOD 成功率從 17.1% 提升到 44.1%，G2-90D 從 13.4% 提升到 31.1%；儘管 G2-90D 資料佔總共訓練資料不到 2%，仍提升 17.7 個百分點，顯示明確的跨具身遷移效果。增益涵蓋 20 個技能群組中的 19 個（G1-OP）與 18 個（G2-90D），且技能特定的資料覆蓋率與零樣本 OOD 成功率的 Pearson 相關係數達 0.80、Spearman 相關係數達 0.85，為業界資料採集投資規劃提供量化依據。同一協議下，模型在至少 90% 試驗中能正確 grounding 物件、顏色、形狀、位置指涉，並能在指令與場景慣性關聯或已承諾行為衝突時仍遵從明確指令，顯示語言理解與動作執行的一致性。

- **結果是否公正**：評測涵蓋 100 項任務、20 個技能群組，且場景、背景、光照、物件實例皆為訓練時未見過（held-out），屬於嚴格的零樣本評測協議而非任務專屬微調後比較，方法論上具備說服力。然而截至目前尚未見第三方獨立復現或跨團隊 benchmark（如 RoboArena）驗證，其「資料規模化曲線」與絕對成功率數字目前僅由 AgiBot 團隊自行報告；且與同為「大規模人類資料規模化」路線的 NVIDIA GEAR DreamDojo（已於本頁 2026-09-10 記錄）相比，兩者資料規模與評測協議不同，尚無法直接類比互證。

- **主要限制**：技術報告尚未標記正式會議接受狀態（僅為 AgiBot Research Team 技術報告），因此「top-conference caliber」準則的滿足程度略低於已確認接受的論文；此外評測雖涵蓋多個技能群組，仍全部基於 AgiBot 自身機器人平台與資料收集流程，尚待第三方在不同機器人本體與資料來源上驗證其資料規模化規律是否普遍成立。

### Related work

- 與本頁「Robot-Specific Action-Conditioned World Models」主題分類已收錄的 τ0-WM（arXiv:2606.01027，同為 AGIBOT 團隊）、Cosmos Policy（arXiv:2601.16163，ICLR 2026）、DreamZero（arXiv:2602.15922，NVIDIA 主導）等論文高度相關，皆探討 world-action model 的架構設計與泛化能力；GE-Act 2.0 與 NVIDIA GEAR 的 DreamDojo（arXiv:2602.06949，同樣強調大規模資料預訓練）在「資料規模化路線」上構成直接對照，值得後續交叉比較兩者在相近評測協議下的表現差異。
- 判斷值得 survey 的程度：中高。GE-Act 2.0 作為 Genie Envisioner 系列（GE-Act）的直接後繼者，若未來釋出更詳細的資料規模化實驗設計或被第三方 benchmark（如 RoboArena）驗證，將是 WAM 資料規模化研究線上一個重要的參照點。

### Conclusion

- **綜合評價**：GE-Act 2.0 提出「WAM 完全從零訓練、獨立於既有影片生成器」的路線，並以嚴謹的零樣本、held-out 評測協議搭配清晰的資料規模化曲線（Pearson r=0.80）驗證了「資料規模」本身對 WAM 泛化能力的直接貢獻，是一篇具備扎實工程投入（100 任務、20 技能群組、300-30,000 小時資料跨度）且方法論清晰的技術報告，值得作為 WAM 資料規模化研究的重要參照。但因尚未見正式會議接受標記，其「top-conference caliber」程度略遜於本頁已收錄的 ICLR/CoRL 級別論文，建議持續追蹤其後續是否被正式會議接受或被第三方 benchmark 驗證。

- **與其他重要文章的關係**：GE-Act 2.0 是 AgiBot 「Genie Envisioner」系列的延伸（與本頁已收錄之 τ0-WM 同源機構），並與 NVIDIA GEAR 的 DreamDojo、EgoScale（同樣強調大規模資料預訓練與規模化規律）構成「資料規模化」路線上的直接對照組；也與本頁基礎模型 Cosmos 3、V-JEPA 2 等通用世界模型路線形成對比——GE-Act 2.0 選擇不繼承通用影片生成器、完全從零在機器人資料上訓練，是與這些通用世界模型路線明確區隔的設計選擇。ROCm/AMD 在此領域尚待補強之處：GE-Act 2.0 的 CoAE/SVP/IDM 三模組聯合訓練涉及大規模影片-動作資料的高吞吐量訓練管線（300 至 30,000 小時級別），目前公開資訊顯示其訓練基礎設施以 NVIDIA GPU 生態為主；AMD 若欲切入 WAM 大規模預訓練基礎設施市場，可考慮驗證 ROCm 上大規模影片編碼/解碼與跨模組聯合訓練（尤其是 KASO 選擇性監督機制所需的動態資料篩選與批次調度）的訓練吞吐量與記憶體效率，作為切入具身智慧基礎設施市場的具體驗證方向。
