---
layout: paper
title: "Embodied Interpretability: Linking Causal Understanding to Generalization in Vision-Language-Action Models"
section: vla
page_id: "1945539823"
permalink: /zh/vla/embodied-interpretability-linking-causal-understanding-to-generalization-in-visi-1945539823/
---

**Paper** : [Embodied Interpretability: Linking Causal Understanding to Generalization in Vision-Language-Action Models](https://arxiv.org/abs/2605.00321)  
**Source** : arXiv / 已被 ICML 2026 (第43屆國際機器學習會議) 接受  
**arXiv ID** : 2605.00321

### Abstract

VLA policy 在分布外情境經常失效,作者推測其原因是模型的決策依賴虛假的視覺關聯而非真正與任務相關的因果線索。本文將「視覺-動作歸因」問題形式化為一個介入性(interventional)估計問題,提出兩個指標:Interventional Significance Score (ISS),透過對視覺區域進行介入式遮罩來估計該區域對動作預測的因果影響;以及 Nuisance Mass Ratio (NMR),衡量模型將注意力歸因到與任務無關特徵的比例純量指標。作者分析了 ISS 的統計性質,證明其可無偏估計,並說明在何種條件下動作預測誤差可作為因果影響的有效代理指標。跨多種操作任務的實驗顯示,NMR 能預測模型的泛化行為,且 ISS 比既有的可解釋性方法產生更忠實的解釋。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945539823_embodied_interp_fig1.png) 

_Figure 1: 透過動作歸因（action attribution）分析 VLA 的泛化能力。以「將其他杯子疊放在紅色杯子上」任務為例，失敗的試驗更依賴無關的視覺線索（如背景、紋理、陰影）做決策；成功的試驗則更依賴任務相關的線索（如機械手臂、末端執行器、杯子）。_

![Figure]({{ site.baseurl }}/assets/images/1945539823_embodied_interp_fig2.png) 

_Figure 2: 本文所提出可解釋性方法總覽。(A) 面板呈現產生介入顯著性分數（Interventional Significance Score, ISS）的管線，透過對多視角觀察施加 Bernoulli 遮罩與高斯混合擾動所誘發的動作差異，聚合成顯著圖，再以線性插值形成連續的 ISS 序列。(B) 面板定義「無關質量比」（Nuisance Mass Ratio, NMR）指標，透過計算 top-k 篩選後的顯著區域與預先定義的無關區段之間的正規化交集，量化策略對非因果特徵的依賴程度。_

  * 要解決的問題:VLA 模型的決策路徑是黑盒,無法確認模型是依賴任務相關的因果視覺線索,還是依賴分布內偶然出現的虛假相關(spurious correlation),這直接關係到模型在分布外(OOD)場景下是否能泛化。
  * 主要方法:把「視覺區域對動作的貢獻」重新定義為介入性估計問題,而非傳統的顯著圖(saliency map)方式。透過對輸入影像的特定區域進行介入式遮罩(intervention/masking),觀察動作輸出的變化,以此計算 ISS;再將模型對「無關(nuisance)」區域的因果歸因加總,得到 NMR 純量。
  * 與以往方法的差異:傳統可解釋性方法(如梯度顯著圖、注意力視覺化)只反映相關性,並非因果性,容易被虛假相關誤導。本文透過介入式(而非觀察式)實驗設計,提供具統計保證(無偏估計)的因果歸因,並進一步證明動作預測誤差在特定條件下可作為因果影響的有效代理,降低了計算介入實驗的成本。
  * 重要方法設計描述:流程大致為:(1) 對輸入影像的視覺區域集合定義遮罩操作;(2) 對每個區域進行介入(替換/遮罩),測量動作分布的變化幅度,得到該區域的因果重要性分數(ISS);(3) 依照任務相關性將區域標記為 task-relevant 或 nuisance,加總 nuisance 部分的歸因得到 NMR;(4) 在多個操作任務的 rollout 上驗證 NMR 與泛化表現的相關性。



### Result

  * 實驗顯示 NMR 能有效預測模型在分布外任務上的泛化行為(NMR 越高,代表模型越依賴無關特徵,泛化能力越差),且 ISS 產生的歸因結果比既有可解釋性方法(如標準的顯著圖方法)更忠實地反映真實因果結構。
  * 是否公正:文中未提供與其他因果歸因方法(如反事實遮罩法、SHAP 等)在相同基準下的直接數值比較細節,摘要僅描述「比既有方法更忠實」,具體數據需要查證全文(需要查證其他論文的比較數據)。



### Limitation

  * 論文摘要未明確列出限制,但方法論上可推測的弱項包括:(1) 介入式遮罩需要對輸入影像做多次前向推論,計算成本可能較高;(2) 定義「task-relevant vs nuisance」的區域劃分是否需要人工標註或啟發式規則,摘要未說明,可能限制其可擴展性;(3) 該方法目前僅在模擬操作任務上驗證,真實機器人硬體上的表現需要進一步查證全文。



### Related work

  * 暫無發現更新的相關研究(截至目前的檢索範圍內未找到明確的後續延伸論文)。
  * 這篇論文與同一 VLA 可解釋性主題下的其他工作(如 Sparse Autoencoders for VLAs、Not All Features Are Created Equal)方向相近,值得一併 survey 以建立完整的 VLA 機制可解釋性圖譜,判斷值得深入追蹤。



### Conclusion

  * 整體評價:本文提出一套具統計保證的因果歸因框架,將可解釋性研究與泛化能力直接掛鉤,是 ICML 2026 接受的工作,方法論嚴謹,對理解 VLA 失效模式有實用價值,值得參考。
  * 與其他重要文章的關係:此文與其他 VLA 可解釋性研究(如 SAE 特徵分析、線性探針方法)互補,前者關注「哪些視覺區域驅動決策」,後者關注「內部激活代表什麼語意」。對 ROCm/AMD 而言,若要在 AMD 硬體上部署 VLA 可解釋性工具鏈(如大量介入式推論、遮罩批次評估),目前看不出論文提及具體的推論框架或硬體最佳化重點,因此看不出與 ROCm 生態系統有明確直接關聯,需要另行評估介入式推論在 ROCm/PyTorch 上的效能是否有優化空間。