---
layout: paper
title: "Artificial Foveated Perception for Mitigating Shortcut Learning in Robotic Foundation Models"
section: vla
page_id: "1972778734"
permalink: /zh/vla/artificial-foveated-perception-for-mitigating-shortcut-learning-in-robotic-found-1972778734/
---

### Abstract

機器人基礎模型部署前仍需任務專屬微調，而微調後的 policy 常在場景佈局、光照或鄰近干擾物略有變化時就失效。本文將這種脆弱性歸因於 shortcut learning：微調只監督動作，卻不監督 policy 用來判斷動作的視覺證據，導致 policy 可能依賴僅能預測示範軌跡、卻與任務成功無因果關係的場景層級相關性（如背景紋理、光照、物件共現、相機偽影）。作者提出 Artificial Foveated Perception（AFP），一個輕量、與 policy 架構無關的模組，接收與既有 VLA/World Action Model pipeline 相同的視覺與語言輸入，預測任務條件化的遮罩，涵蓋相關物件、機器人本體與其他動作關鍵區域。微調期間，此遮罩作為輔助 grounding 訊號，將 policy 的視覺注意力對齊到任務相關區域；policy 架構本身不變，推論時僅使用原始觀測串流，不呼叫 AFP。在模擬環境中對 SmolVLA、OpenVLA、π0.5 與 Motus 四個基礎模型、八項 MimicGen 任務，以及真實機器人上以 π0.5 進行五項任務（來自 FurnitureBench 與自建場景）的評測顯示，AFP 在環境擾動下提升泛化能力、降低過擬合，並縮短長 horizon 任務的微調時間。消融實驗（遮罩品質、grounding loss 設計）證實增益確實來自將 policy 學習導向任務相關視覺證據，而非其他副作用。已被 CoRL 2026 接受。

### Method

- **要解決的問題**：機器人基礎模型的微調流程只以動作標籤監督學習信號，完全沒有約束 policy 依賴哪些視覺線索；因此 policy 容易學到「shortcut」——僅在訓練場景中恰好與示範動作相關、但對任務成功無因果貢獻的視覺相關性（背景紋理、光照條件、物件共現、相機偽影等）。這類 shortcut 在訓練分布內表現正常，一旦場景佈局、光照或加入分心物件（distractor）等環境擾動發生，policy 立即失效。

- **Main method**：AFP 是一個獨立、輕量、policy-agnostic 的任務條件化遮罩預測器。其架構分為兩條路徑：(1) Feature path——以 MobileNetV3-Large 骨幹取得多尺度特徵金字塔，每一層級投影、攤平為視覺 token 後送入 deformable transformer encoder；(2) Query path——少量可學習的區域查詢（region queries）透過 deformable cross-attention 對視覺記憶解碼，作為任務相關物件與末端執行器的緊湊描述子，並以時序模組維持跨幀遮罩穩定性。語言條件則透過凍結的 CLIP 文字嵌入驅動 FiLM adapter，對解碼後的查詢做 scale/shift/gate 調變（而非將文字直接串接為 token）。最終 mask head 將多尺度特徵融合為高解析度圖，主要查詢與每個空間位置匹配後經 sigmoid 得到連續遮罩 M_t ∈ [0,1]^(H×W)。微調期間，讀取 policy 對影像 token 的注意力，於可訓練層/頭/查詢位置上平均後與池化後的 AFP 遮罩比較，兩側正規化後計算 grounding loss L_AFP，最終以 L = L_act + λ·L_AFP 聯合訓練。為避免 grounding 訊號與動作學習的梯度衝突，採用類似 PCGrad 的投影梯度機制：當 AFP 梯度方向與動作梯度相反時，去除其衝突分量後再更新（實驗中 20k 微調步驟內觸發 11,152 次投影，若無此機制訓練損失會在過半訓練後劇烈上升）。

- **和以往方式的差異**：以往將 tactile/vision 多模態訊號整合進 policy 的做法，或既有的 VLA/WAM 微調範式，都是在動作層級做監督，沒有機制對「policy 為何做出此動作所依賴的視覺證據」施加任何約束或修正。AFP 首次將「fine-tuning 期間對齊 policy 視覺注意力」重新定義為一個獨立的輔助監督問題，且刻意設計為推論時完全不參與（inference-time zero overhead）、不需修改 policy 本身架構，這與需要修改 policy 架構或在推論迴圈中引入額外運算的方案（如需在控制迴圈內持續呼叫的模組）形成明確區隔。

- **重要方法截圖**：見下方嵌入圖片——Figure 1 展示 AFP 如何透過抑制分心物件、將注意力導向任務相關區域來緩解 shortcut learning；Figure 2（架構圖）展示 Feature path / Query path / 語言 FiLM 調變 / Mask head 的完整資料流。

![Figure]({{ site.baseurl }}/assets/images/2607.10655_afp_teaser.png)

_Figure 1: AFP 透過抑制分心物件、將注意力導向任務相關區域來緩解 shortcut learning_

![Figure]({{ site.baseurl }}/assets/images/2607.10655_afp_architecture.png)

_Figure 2: AFP 架構圖 — Feature path 與 Query path 搭配 CLIP FiLM 語言調變與 mask head_


### Result

- **主要增強部分**：在八項模擬 MimicGen 任務、四種基礎模型（SmolVLA、OpenVLA、π0.5、Motus）上，AFP 讓 π0.5 的 in-distribution Soft-IoU 從 0.17（直接微調）提升至 0.93，EMD 從 4.39 降至 0.04，顯示注意力確實被拉回人類標註的任務相關區域；分佈外（加入 3-5 個未見過的 RoboSuite 物件作為干擾物）成功率全面提升，且在分佈內設定下 AFP 至少持平或優於直接微調（未犧牲原有表現）。真實世界以 π0.5 在 i2RT YAM Arm 上進行五項任務（含 FurnitureBench 的 Drawer/Lamp/Table Assembly、Cloth Folding、Closet Storage）驗證，AFP 在分佈內外皆全面提升，且分佈外增益最大。此外，在長 horizon、多階段任務（Kitchen、Coffee Preparation、Three Piece Assembly）上，AFP 訓練的 policy 明顯更快達到高成功率，短任務上增益則較不明顯，顯示增益與「觀測串流中與任務無關比例」正相關。

- **結果是否公正**：論文在四種不同架構（自迴歸、diffusion/flow-matching 等不同動作頭設計）的基礎模型與模擬+真實雙軌評測上都做了驗證，且消融實驗（遮罩品質、grounding loss 設計、有無投影梯度）系統性地拆解了增益來源，具備合理的科學嚴謹度。官網與論文皆提供程式碼、標註工具與資料集（Hugging Face），可供第三方重現。目前未見其他論文對此方法提出直接反駁或不一致的結果，但由於是新發表尚未歷經廣泛第三方復現週期。

### Limitation

- **已知 limitation**：AFP 依賴人類標註的任務相關性遮罩才能訓練——需要人類在少量關鍵幀上標註 point prompt，再透過 SAM 2 + MatAnyone 傳播至整個序列，這帶來額外標註成本與潛在標註偏誤。當任務相關性本身模糊、物件嚴重遮擋，或場景超出遮罩資料集分布時，AFP 可能失效。

- **從 result 來看的弱項**：論文坦承的兩個延伸方向（擴大標註資料集規模、或改由互動/時序一致性/反事實場景變化/policy 失敗案例中自動學習相關性而非依賴人類標註）本身就暗示目前方法在資料規模化與標註自動化上仍有明顯瓶頸；此外真實世界驗證僅限單一機械手臂平台（i2RT YAM Arm）與五項任務，跨具身可遷移性尚待更廣泛驗證。

### Related work

- arXiv 上與此方向高度相關的既有工作包括 shortcut learning 在視覺表徵學習中的一般性研究，以及既有的 attention-alignment/grounding 輔助損失方法；本頁 VLA Papers 中「Interpretability & Diagnostics」主題分類下已收錄的 Sparse Autoencoders Reveal Interpretable and Steerable Features（2603.19183）與 Not All Features Are Created Equal（2603.19233）等論文分析 VLA 內部視覺/語言路徑的機制性行為，與 AFP 探討「policy 依賴何種視覺證據」屬互補視角，值得交叉參照。
- 判斷值得 survey 的程度：中高。AFP 提出的「fine-tuning 期間對齊注意力、推論時零額外開銷」範式具有跨架構、跨具身的可遷移潛力，且已釋出完整程式碼、標註工具與資料集，後續若有其他團隊在其資料集上驗證或擴展至更多基礎模型/真實平台，將是值得持續追蹤的方向。

### Conclusion

- **綜合評價**：AFP 提出的問題診斷（shortcut learning 源於微調僅監督動作而非視覺證據）精準且具普遍性，解法設計簡潔（inference-time 零開銷、policy-agnostic），並在四種代表性基礎模型與模擬+真實雙軌上做了扎實驗證，同時開源程式碼、標註工具與資料集，是一篇值得參考的 CoRL 2026 論文，尤其對任何正在為機器人基礎模型做落地部署微調的團隊都有直接參考價值。

- **與其他重要文章的關係**：AFP 與本頁「Interpretability & Diagnostics」主題（Sparse Autoencoders、Not All Features Are Created Equal、Decoding Task Progress、Tri-Info）共享「理解/診斷 VLA 內部視覺-語言路徑」的關注點，但 AFP 更進一步地將診斷結果轉化為可直接改善下游泛化的訓練時介入手段；也與本頁基礎模型 π0.5（arXiv:2604.15483）直接相關，因為 AFP 的真實機器人實驗即以 π0.5 作為驗證骨幹之一。ROCm/AMD 在此領域尚待補強之處：目前 AFP 的訓練與推論皆以 NVIDIA GPU 生態（PyTorch + CUDA 加速的 deformable attention/transformer 運算）為預設環境，尚未見到針對 ROCm 的 deformable attention 算子最佳化或跨平台基準測試；由於 AFP 本身推論時零額外開銷、僅在訓練期間引入運算負擔，若 AMD 欲切入機器人基礎模型微調基礎設施市場，可考慮驗證 deformable transformer + FiLM 語言調變在 ROCm 上的訓練效能與數值穩定性，作為後續生態系拓展的具體切入點。
