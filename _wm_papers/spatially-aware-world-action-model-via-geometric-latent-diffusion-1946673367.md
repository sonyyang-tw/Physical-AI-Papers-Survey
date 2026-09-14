---
layout: paper
title: "Spatially Aware World Action Model via Geometric Latent Diffusion"
section: wm
page_id: "1946673367"
permalink: /wm/spatially-aware-world-action-model-via-geometric-latent-diffusion-1946673367/
---

### Abstract

World Action Models (WAMs)利用大規模預訓練的影片擴散模型，同時預測未來觀測與動作，繼承了網路規模影片中豐富的視覺與物理先驗知識，是機器人策略學習的一個有前景的範式。然而現有方法幾乎都只在 RGB 觀測上操作，未能利用 3D 資訊。本文提出 Spatially Aware World Action Model (SA-WAM)，將預訓練的影片模型改造為可同時預測動作、RGB 與深度的模型，在單一擴散骨幹網路中實現具 3D 感知能力的世界建模與動作預測。作者設計了一種非線性編碼，將無界的深度訊號映射到凍結 VAE tokenizer 所預期的有界輸入域，使得無需針對 3D 進行專門微調即可重複利用該 tokenizer，在不犧牲預訓練先驗的前提下納入幾何資訊。SA-WAM 在 RoboCasa 與 LIBERO-Plus benchmark 上取得 state-of-the-art 結果，同時提升了未來狀態的預測品質；此外在真實世界 UR5 機械臂評測中，於隨機化環境下相較強基準有顯著提升。作者也分析了世界模型預測品質與 rollout 成功率之間的相關性，為 WAM 的效能與改進方向提供了洞見。

![Figure]({{ site.baseurl }}/assets/images/1946673367_diagram_sa-wam.png) ![Figure]({{ site.baseurl }}/assets/images/1946673367_robocasa_fig3.png) 

### Method

  * **要解決的問題** ：現有的 World Action Models（如 Cosmos-Policy 一類方法）都只在 RGB 觀測空間運作，缺乏顯式的 3D/深度資訊，導致對物體幾何與空間關係的建模能力受限，進而限制策略在真實世界隨機化場景下的泛化與抓取精度。


  * **Main method** ：SA-WAM 將一個預訓練的影片擴散模型（Diffusion Transformer, DiT）改造為「聯合 action、RGB、depth 預測」模型。具體做法是把 proprioception（本體感覺 q_t）與 action chunk（a_t）直接插入 latent 序列中的專屬位置；條件訊號包含任務描述（task）、每個視角的一張 RGB frame（v_t^c）與其對應的 3D 模態（深度 g_t^c）交錯排列，以及當下時刻的本體感覺資訊。深度訊號透過一種非線性編碼方式映射進凍結的 VAE tokenizer 所預期的有界輸入域，因此可以直接重複使用同一個 RGB 用的 VAE tokenizer 來處理深度，而不需要額外的 3D 專用 encoder 或針對 3D 進行 tokenizer 微調。去噪（denoising）過程作用在 action chunk、未來 RGB（v_t'^c）與未來深度（g_t'^c）之上；解碼階段在推論時是可選的。


  * **和以往方式的差異** ：先前的 WAM（例如 Cosmos-Policy）僅利用 RGB 影片先驗做動作與未來影格的聯合預測，完全沒有幾何/深度資訊；SA-WAM 首次把深度模態以「不改變凍結 VAE tokenizer」的方式無縫塞進同一個擴散骨幹，因此能同時保留大規模影片預訓練帶來的視覺先驗，又新增了 3D 空間感知能力，是一種「以最小改動獲得幾何感知」的設計。


  * 論文包含兩張重要截圖：Fig. 1（RoboCasa benchmark 上的 SOTA 結果對比圖）與 Fig. 2（SA-WAM 整體架構圖，展示 RGB/深度/proprioception/action 在 latent 序列中的排列方式）。



### Result

  * 在 RoboCasa benchmark 上，僅用每個任務 50 筆示範（demonstration），SA-WAM 達到 76.6% 成功率，比對照的 Cosmos-Policy baseline 高出 9.5 個百分點，並且超越了以往需要 6–20 倍示範資料量的方法。
  * 在 LIBERO-Plus benchmark 上同樣達到 state-of-the-art 結果（摘要中未列出具體數字，需要查證論文正文以取得精確分數）。
  * 在真實世界 UR5 機械臂評測中，SA-WAM 在隨機化環境設定下相較強基準有明顯提升（摘要與正文片段未提供精確百分比，需要查證全文表格）。
  * 論文同時分析了世界模型預測品質（world modeling quality）與策略 rollout 成功率之間的相關性，提供了理解 WAM 效能與未來改進方向的依據；Fig. 3 展示 RoboCasa 上一個「pick-and-place」任務的定性比較，Cosmos-Policy 與 SA-WAM 的 wrist-view rollout 與模擬器 rollout 對照，紅框標示 rollout 不一致之處，綠框標示任務完成。


  * **result 是否公正** ：三位作者中包含 Google DeepMind 研究員 Cordelia Schmid，實驗設計包含模擬（RoboCasa、LIBERO-Plus）與真實機器人（UR5）雙重驗證，且與同期強基準 Cosmos-Policy 做了直接對照，可信度較高；但目前僅有本論文自身報告的數字，尚無第三方復現或其他論文的交叉驗證，需要持續關注後續是否有其他工作复現或質疑其結果。



### Limitation

  * 論文摘要與可讀取的正文片段中未明確列出限制章節的具體內容，需要查證全文（尤其是 Discussion/Limitation 段落）以取得完整資訊。
  * 從方法設計上可推測的潛在限制：(1) 深度資訊的取得仍依賴模擬器或深度感測器，真實部署時深度品質可能受感測器雜訊影響；(2) 非線性深度編碼方式雖然重用了既有 VAE tokenizer，但對於超出訓練分佈範圍的深度值（例如極端遠近距離）可能仍有失真風險；(3) 目前驗證的真實世界機器人平台僅為 UR5 單一機械臂，尚未展示在更多樣化 embodiment（如人形機器人、雙臂系統）上的可遷移性。
  * 從 result 來看，論文並未提供 LIBERO-Plus 與真實世界 UR5 實驗的精確數字（僅摘要性描述「state-of-the-art」與「strong gains」），這使得與其他方法的量化比較上不夠透明，是本篇論文在報告完整性上的弱項。



### Related work

  * 直接對照基準為 Cosmos-Policy（NVIDIA Cosmos 系列的 policy fine-tuning 工作），屬於同一時期最重要的 World Action Model 相關工作之一。
  * arXiv 近期（2609.xxxxx / 2608.xxxxx）出現多篇同屬 World Action Model / Embodied World Model 路線的論文，例如 GeniWorld (2608.06332)、XEWorld (2608.05799)、RoboPhys-3D (2608.28718) 等，顯示「action-conditioned / 3D-aware world model」正是 2026 下半年機器人學習領域的熱門方向，值得持續追蹤。
  * 判斷值得 survey 的程度：高。此論文由 Google DeepMind 研究員參與，方法論上首次以「不改動凍結 tokenizer」的方式引入深度模態，具有清晰的架構創新，且同時提供模擬與真實機器人雙重驗證，代表了 World Action Model 從純 RGB 走向 3D 感知的一個重要階段性進展。



### Conclusion

  * 整體評價：這是一篇具有紮實方法創新與跨模擬/真實驗證的論文，出自 Google DeepMind 研究員參與的團隊，在 RoboCasa 與 LIBERO-Plus 兩個主流機器人操作 benchmark 上都取得 SOTA，並透過真實 UR5 機械臂驗證了 sim-to-real 的可行性，值得作為 World Action Model 3D 化路線的重要參考文獻。
  * 與其他重要文章的關係：SA-WAM 建立在 Cosmos-Policy（RGB-only WAM baseline）之上，並與同期的 GeniWorld、XEWorld 等「action-conditioned world model 泛化性」研究方向互補——後者關注跨 embodiment 泛化，SA-WAM 關注跨模態（RGB+depth）幾何感知，兩條路線未來有機會匯流成「跨 embodiment、跨模態」的下一代 World Action Model。
  * ROCm/AMD 在此領域尚待補強的部分：目前 SA-WAM 的訓練與推論管線建立在 NVIDIA 生態（Cosmos-Policy 對照、及業界普遍使用的 CUDA-based 影片擴散訓練框架）之上；AMD/ROCm 若要切入此類「影片擴散 + 深度聯合建模」的 World Action Model 訓練，需要驗證 ROCm 上大規模影片 Diffusion Transformer（DiT）訓練的穩定性與吞吐量，並補強對應的深度模態資料前處理與 VAE tokenizer 移植，才能在真實機器人 world model 訓練場景中提供具競爭力的替代方案。