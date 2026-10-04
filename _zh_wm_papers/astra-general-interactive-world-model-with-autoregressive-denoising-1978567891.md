---
layout: paper
title: "Astra: General Interactive World Model with Autoregressive Denoising"
section: wm
page_id: "1978567891"
permalink: /zh/wm/astra-general-interactive-world-model-with-autoregressive-denoising-1978567891/
---

### Abstract

Astra（arXiv:2512.08931，ICLR 2026 接受，清華大學與快手科技 Kuaishou Technology 合作，作者包含 Xin Tao、Pengfei Wan 等快手可靈 Kling 團隊資深研究者）提出一個通用互動式 world model 框架，能針對多種場景（自駕、機器人抓取等）生成具備精確動作互動（相機運動、機器人動作）的真實世界未來影格。核心方法為自迴歸去噪 (autoregressive denoising) 架構：以時間因果注意力聚合過去觀測並支援串流輸出，搭配「噪聲增強歷史記憶」(noise-augmented history memory) 平衡回應性與時間一致性；並以動作感知適配器 (action-aware adapter) 將動作訊號直接注入去噪過程，再輔以混合動作專家 (Mixture of Action Experts, MoAE) 動態路由異質動作模態。實驗橫跨 Sekai、SpatialVID、RT-1、nuScenes、Multi-Cam Video 等多個資料集，證明 Astra 在保真度、長距離預測與動作對齊上優於既有 state-of-the-art world model。

### Method

**要解決的問題**：現有影片生成模型（T2V/I2V）僅能產生短暫、自成一體的影片片段，無法產生對外部刺激（智能體移動、視角變化、控制訊號）動態回應的長 horizon 一致 rollout，因而無法真正模擬世界的互動性與因果動態；既有的自迴歸延伸方法則難以兼顧「保持與歷史幀一致」與「即時回應新輸入」，且自迴歸生成過程存在誤差累積問題，導致長期預測品質與一致性下降。

**Main method**：Astra 以預訓練影片擴散骨幹（基於 Wan2.1-1.3B）為基礎，提出自迴歸去噪架構：用時間因果注意力聚合過去觀測、支援串流輸出；提出「噪聲即遮罩」(noise-as-mask) 策略，訓練時對歷史幀施加柔性噪聲腐蝕，削弱視覺歷史脈絡的主導性，迫使模型同時整合歷史與動作線索來預測下一影片區塊；設計輕量的 ACT-Adapter（動作感知適配器），凍結大部分預訓練參數、僅微調 adapter 與注意力層，將動作訊號直接注入去噪過程；並提出 Mixture of Action Experts (MoAE)，以可學習路由機制動態調度異質動作模態（相機控制、身體姿態、機器人操作）至各模態專屬專家，統一多種互動訊號於單一框架。

**和以往方式的差異**：與既有影片延伸/混合自迴歸+擴散框架（如 he2025matrix 的 cross-attention adapter）相比，ACT-Adapter 消融實驗證明其動作條件化效果優於既有交叉注意力適配器；「噪聲即遮罩」策略明確針對「視覺慣性」(visual inertia，模型傾向單純外推歷史幀而忽略動作輸入) 問題設計，是與既有方法僅靠架構調整平衡一致性與回應性不同的訓練策略創新；MoAE 首次以路由機制統一處理跨領域（自駕、機器人、開放世界探索）異質動作模態，而非針對單一領域客製化動作條件化方式。

**關鍵方法圖**：Figure 1 展示 Astra 跨探索、機器人操作、自動駕駛三大場景的互動式 world modeling 能力總覽；Figure 3 展示自迴歸去噪架構的完整 pipeline，包含時間因果注意力、噪聲增強歷史記憶與 ACT-Adapter 如何協同運作。

![Figure]({{ site.baseurl }}/assets/images/2512.08931_astra_teaser.png)

_Figure 1: Astra 跨探索、機器人操作、自動駕駛場景的互動式 world modeling 總覽_

![Figure]({{ site.baseurl }}/assets/images/2512.08931_astra_pipeline.png)

_Figure 2: Astra 自迴歸去噪架構完整 pipeline——時間因果注意力、噪聲增強歷史記憶與 ACT-Adapter_

### Result

**Result 結果如何**：在自建的 Astra-Bench 上，與 Wan-2.1、Matrix-Game、YUME 等 state-of-the-art 影片生成/world model 方法比較，Astra 在視覺品質指標（主體/背景一致性、動作流暢度、整體美學）與動作條件化回應性（人類評估確認生成軌跡更忠實跟隨相機運動與動作指令方向）上全面勝出；在長距離 rollout 下，既有方法常見誤差累積與畫面漂移，Astra 則能維持穩定性。消融實驗證實：ACT-Adapter 優於既有 cross-attention adapter 設計；action-free guidance 機制能放大動作訊號對推論的影響，尤其提升長影片 rollout 中的動作回應性；噪聲即遮罩策略確實緩解視覺慣性問題，讓模型對突發或非預期動作有更強回應同時保持長期時間一致性。

**Result 是否公正**：論文提供了完整消融實驗拆解各元件（ACT-Adapter、action-free guidance、noise-as-mask、MoAE）的個別貢獻，並在多個獨立公開資料集（Sekai、SpatialVID、RT-1、nuScenes、Multi-Cam Video）上驗證，涵蓋自駕與機器人操作等不同應用場景，泛化驗證較為完整；且已通過 ICLR 2026 同行評審。惟比較基準 Astra-Bench 為作者自建，其評測協定與既有社群標準 benchmark（如機器人領域常見的成功率評測）尚待更廣泛社群採用與交叉驗證。

### Limitation

**已知的 limitation**：論文明確設立「Limitations」章節，坦承推論效率仍是主要瓶頸——由於架構建立在擴散式生成之上並採自迴歸 rollout，產生長 horizon 互動影片需要每幀多步去噪，使即時部署面臨挑戰，尤其限制其在線上控制或互動式機器人等延遲敏感場景的應用；作者提出未來可透過蒸餾或師生壓縮策略降低推論成本，同時保留 Astra 的保真度與回應性。

**從 result 來看的弱項**：儘管 MoAE 讓 Astra 能跨領域統一處理異質動作模態，論文亦提及跨異質資料集聯合訓練可能略微降低模型在單一特定場景下的表現，顯示「通用性」與「單一場景最佳化」之間仍存在取捨；此外附錄雖有討論「視覺慣性」現象，但對於何種動作類型或場景下噪聲即遮罩策略效果最弱，論文未見更細緻的失效案例分析。

### Related work

與本頁「Robot-Specific Action-Conditioned World Models」子主題下已收錄的 τ0-WM、Pelican-Sim 1.0、GE-Act 2.0、GeniWorld 等論文同屬「以統一架構處理跨具身/跨場景動作條件化」的方法論脈絡，但 Astra 進一步將適用範圍擴展至自駕與開放世界探索等非機器人操作場景，是本頁目前唯一同時涵蓋機器人操作、自動駕駛、開放世界探索三大應用的通用互動式 world model；其「自迴歸去噪 + 動作感知適配器」設計與本頁「World Models for Autonomous Driving」子主題下的 DriVerse、GAIA 系列亦有場景重疊，可作為跨主題橋接論文。

值得 survey 的程度：高。Astra 提出的「噪聲即遮罩」訓練策略與 MoAE 路由機制皆為本頁尚未收錄的具體技術創新，且獲 ICLR 2026 正式接受，作者陣容含快手可靈（Kling）團隊核心成員，代表工業界對通用互動式 world model 的持續投入，值得追蹤其後續在推論效率優化（如蒸餾）上的進展。

### Conclusion

**綜合評價**：Astra 提出了一個方法論明確、跨場景通用的互動式 world model 框架，自迴歸去噪架構、噪聲即遮罩策略、ACT-Adapter 與 MoAE 四項元件皆有清楚的問題動機與消融驗證，且已通過 ICLR 2026 審稿，是本頁「Robot-Specific Action-Conditioned World Models」與「World Models for Autonomous Driving」跨主題下值得記錄的重要進展。

**與其他重要文章的關係**：與本頁基礎模型 Genie 3、Cosmos 3、GAIA 系列同屬「通用世界模擬器」路線，但 Astra 更聚焦於「動作互動的精確性與跨模態統一」；其自迴歸去噪與噪聲增強歷史記憶設計，也與本頁「Model-Based RL / Latent Dynamics for Control」子主題中 DreamerV3 的時間一致性建模理念有相通之處。ROCm/AMD 待補強：Astra 論文本身已指出推論效率（多步去噪 + 自迴歸 rollout）是主要部署瓶頸，這類「凍結骨幹 + 輕量 adapter 微調」的訓練範式與長 horizon 自迴歸推論管線，在 ROCm 上的算子融合與 KV cache 管理效能調校目前公開資料有限，是 AMD 在互動式 world model 推論加速上可切入的方向。
