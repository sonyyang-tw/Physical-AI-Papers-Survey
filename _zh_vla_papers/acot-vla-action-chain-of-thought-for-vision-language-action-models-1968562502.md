---
layout: paper
title: "ACoT-VLA: Action Chain-of-Thought for Vision-Language-Action Models"
section: vla
page_id: "1968562502"
permalink: /zh/vla/acot-vla-action-chain-of-thought-for-vision-language-action-models-1968562502/
---

### Abstract

ACoT-VLA（arXiv:2601.11404，CVPR 2026 接受，AgiBot）提出「Action Chain-of-Thought」(ACoT) 範式：讓 VLA 的推理過程直接在動作空間中進行，而非依賴語言子任務預測或目標影像合成等間接中介表示。作者觀察到既有的顯式中介推理（語言子任務、視覺目標影像）對精確動作執行所需的細粒度資訊傳達能力有限。ACoT-VLA 架構由兩個互補元件組成：Explicit Action Reasoner (EAR) 提出粗粒度參考軌跡作為顯式動作層級推理步驟，Implicit Action Reasoner (IAR) 則從多模態輸入的內部表示中萃取隱式動作先驗，兩者共同構成 ACoT 並用以條件化下游動作頭，實現有根據的策略學習 (grounded policy learning)。真實世界與模擬環境的大量實驗證明此方法優於既有 baseline，程式碼已於 GitHub 開源 (AgibotTech/ACoT-VLA)。

### Method

**要解決的問題**：傳統 VLA 直接將多模態輸入透過 VLM embedding 映射到動作，缺乏顯式推理步驟；近期方法雖引入語言子任務預測或目標影像合成作為中介推理，但這類間接表示本質上難以承載精確動作執行所需的完整、細粒度資訊。

**Main method**：提出 Action Chain-of-Thought (ACoT) 範式，主張最有效的推理應直接在動作空間中進行。具體架構包含：(1) Explicit Action Reasoner (EAR)：一個 Transformer 模組，提出粗粒度參考軌跡作為顯式動作層級推理步驟；(2) Implicit Action Reasoner (IAR)：從共享 VLM backbone 的內部特徵中萃取隱式動作先驗；兩者的輸出共同構成 ACoT，並條件化最終的動作生成頭，使動作生成具備可追溯的推理鏈。

**和以往方式的差異**：與 Language CoT（如 LoHoVLA、DualCoT-VLA 等，以語言子任務作中介）及 Visual CoT（以合成目標影像作中介）不同，ACoT-VLA 的推理直接發生在動作空間（粗粒度軌跡），避免了語言/影像中介表示在傳達精細動作資訊時的損失，是本頁尚未收錄的第三種 CoT 空間路線。

**關鍵方法圖**：Figure 1 對比三種 CoT 範式（語言空間、視覺空間、動作空間）；Figure 2 展示 ACoT-VLA 完整架構，包含共享 VLM backbone 上的 EAR 與 IAR 雙模組如何共同條件化下游動作頭。

![Figure]({{ site.baseurl }}/assets/images/2601.11404_acot_fig1.png)

_Figure 1: 三種 CoT 範式對比（語言空間、視覺空間、動作空間）_

![Figure]({{ site.baseurl }}/assets/images/2601.11404_acot_fig2.png)

_Figure 2: ACoT-VLA 完整架構 — EAR 與 IAR 雙模組如何共同條件化下游動作頭_

### Result

**Result 結果如何**：論文在真實世界與模擬環境中進行大量實驗，顯示 ACoT-VLA 優於既有 VLA baseline（包含直接映射與既有語言/視覺 CoT 方法）；已被 CVPR 2026 接受，顯示同行評審認可其實驗完整度與貢獻度。

**Result 是否公正**：由於原文為 CVPR 接受版本，實驗設計與比較基線應已通過審稿把關；但本次 harness 僅取得 arXiv 摘要與 HTML 版本的公開描述，未逐一核對其真實機器人任務數量與具體成功率數字是否與其他論文（如本頁已收錄的 LoHoVLA、DualCoT-VLA）在相同 benchmark 下可直接比較，此處無法斷言其結果與其他論文結果是否完全一致。

### Limitation

**已知的 limitation**：論文摘要與方法描述未明確揭露 EAR 提出的「粗粒度參考軌跡」在複雜長 horizon 任務中累積誤差的風險，亦未討論 EAR 與 IAR 兩路徑推理不一致時的容錯機制。

**從 result 來看的弱項**：作為 CVPR 2026 論文，摘要層級的描述較為精簡，實驗細節（如具體評測任務清單、跨具身泛化能力）需要查閱全文才能進一步評估；本頁記錄僅能反映摘要層級資訊。

### Related work

arXiv 上更新的 related work：本頁已收錄的 DualCoT-VLA (2603.22280)、DeepThinkVLA (2511.15669)、Latent Reasoning VLA (2602.01166) 皆屬語言/latent CoT 路線，與 ACoT-VLA 的「動作空間 CoT」路線形成對照，值得交叉比對三種 CoT 空間的優劣。

值得 survey 的程度：高。ACoT 提出的「動作空間推理」是一個相對新穎且尚未被本頁充分覆蓋的子方向，後續若有更多論文延伸此路線（例如結合 world model 對動作軌跡做前瞻校驗），值得持續追蹤。

### Conclusion

**綜合評價**：ACoT-VLA 提出了一個概念清晰、方法論上具區隔性的新 CoT 範式（動作空間推理 vs. 既有語言/視覺空間推理），且已通過 CVPR 2026 審稿，出自 AgiBot 這類具規模的機器人研究團隊，值得列入 VLA 階層式推理/CoT 子主題的參考文獻。

**與其他重要文章的關係**：與本頁「Hierarchy: High-Level Planning/Reasoning」主題下的 LoHoVLA（統一 backbone 做高低階規劃）、DualCoT-VLA（平行視覺+語言 CoT）、Latent Reasoning VLA（latent CoT）構成同一問題空間下的不同解法譜系；ACoT-VLA 的「動作空間 CoT」可視為對既有語言/視覺 CoT 路線的方法論補完。ROCm/AMD 待補強：目前開源社群對 VLA 動作頭的訓練與推論加速多聚焦於 diffusion/flow-matching 動作頭，ACoT-VLA 這類「雙推理器（EAR+IAR）+ 動作頭」的三段式架構對推論管線的分段最佳化（尤其 EAR 的自迴歸粗軌跡生成與 IAR 的隱式特徵萃取如何在 ROCm 上高效並行）目前公開資料有限，是 AMD 在此類階層式 VLA 推論優化上可切入的方向。
