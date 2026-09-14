---
layout: paper
title: "VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks"
section: vla
page_id: "1945474246"
permalink: /vla/vlabench-a-large-scale-benchmark-for-language-conditioned-robotics-manipulation--1945474246/
---

**Paper** : [VLABench: A Large-Scale Benchmark for Language-Conditioned Robotics Manipulation with Long-Horizon Reasoning Tasks](https://arxiv.org/abs/2412.18194)  
**Source** : arXiv (cs.RO); ICCV 2025 (accepted, poster)  
**arXiv ID** : 2412.18194

### Abstract

通用型具身智能體被設計來理解使用者的自然語言指令或意圖,並精確執行動作以完成通用任務。近期,以基礎模型為基礎的方法,特別是 Vision-Language-Action（VLA）模型,已展現出解決語言條件操作（Language-Conditioned Manipulation, LCM）任務的顯著潛力。然而,現有的 benchmark 並未充分滿足 VLA 及相關演算法的需求。為了在大型語言模型的脈絡下更好地定義這類通用任務,並推進 VLA 研究,作者提出 VLABench,一個開源的 benchmark,用於評估通用 LCM 任務學習。VLABench 提供 100 個精心設計的任務類別,每個類別內都有高強度的隨機化,總共涵蓋 2000 多個物件。VLABench 在四個關鍵面向上有別於既有 benchmark:(1) 需要世界知識與常識遷移的任務;(2) 使用蘊含隱含人類意圖的自然語言指令,而非樣板化指令;(3) 需要多步驟推理的長時程任務;(4) 同時評估動作策略與語言模型能力。此 benchmark 評估多項能力,包括對網格與紋理的理解、空間關係、語意指令、物理定律、知識遷移與推理等。為支援下游微調,作者也提供透過自動化框架（結合啟發式技能與先驗資訊）收集的高品質訓練資料。實驗結果顯示,目前最先進的預訓練 VLA 模型以及基於 VLM 的工作流方法,在此 benchmark 的任務上都面臨挑戰。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945474246_vlabench_fig1.png) 

_Figure 1: VLABench overview._

![Figure]({{ site.baseurl }}/assets/images/1945474246_vlabench_fig6.png) 

_Figure 6: VLABench evaluation workflow._

  * 要解決的問題：既有的機器人操作 benchmark 無法充分滿足 VLA 及相關演算法的評測需求——例如缺乏世界知識與常識遷移的考驗、指令多為固定樣板而非蘊含隱含意圖的自然語言、任務多為單步驟而非長時程多步驟推理、且通常只評估動作策略而不評估語言理解能力。
  * Main method：VLABench 建構了一個涵蓋 100 個任務類別、2000 多個物件的大規模模擬 benchmark,並在每個任務類別內加入高強度隨機化,以避免模型透過記憶樣板而非真正理解取巧。任務設計特意涵蓋四個以往 benchmark 較少強調的面向：世界知識/常識遷移、隱含意圖的自然語言指令、需要多步驟推理的長時程任務,以及同時評估動作策略與語言模型能力的雙軌評測。此外,作者提供一套自動化資料收集框架（結合啟發式技能與先驗資訊）,用於生成高品質的下游微調訓練資料。
  * 和以往方式的差異：與以往 benchmark（任務多為短時程、指令樣板化、僅評估動作成功率）不同,VLABench 刻意將任務設計得更貼近真實世界的模糊性與複雜度——指令蘊含隱含人類意圖而非明確樣板、任務需要多步驟長時程推理、且評測範圍擴及語言/視覺理解能力。
  * 重要方法設計描述：整體 benchmark 可以想像成兩層任務結構——Primitive Tasks（基礎任務,60個,只需一到兩個維度的能力與少量技能組合,例如單一抓取或放置動作）與 Composite Tasks（組合任務,40個,需要多步驟推理與長時程規劃,涉及更多技能與能力的組合）。評測框架進一步分為三大類：對預訓練或微調後 VLA 模型的評估、整合基礎模型與各種演算法的啟發式工作流評估,以及對視覺語言模型（VLM）在多維度能力上的評估（如 mesh/紋理理解、空間關係、物理定律推理）。



### Result

  * 實驗結果顯示,目前最先進的預訓練 VLA 模型與基於 VLM 的工作流方法,在 VLABench 的任務上都面臨顯著挑戰（摘要未提供具體成功率數字,需查證全文的實驗表格）。
  * 主要增強/揭露的部分：此 benchmark 主要增強的並非某個模型的性能,而是評測維度的完整性——揭露了現有 VLA 模型在長時程推理、隱含意圖理解、世界知識遷移等方面的普遍不足。
  * 是否公正：作為 ICCV 2025 正式接受的論文,已經過同行評審把關;但由於是新提出的 benchmark,其任務設計是否存在對特定模型架構的隱性偏好,需要查證全文與第三方評測結果,暫無法確認是否有與其他論文結果不符之處。



### Limitation

  * 摘要中沒有明確自陳的 limitation 段落,需要查證全文。
  * 從實驗結果推測的潛在弱項：現有 SOTA VLA 模型與 VLM 工作流都在此 benchmark 上遇到困難,意味著任務難度可能偏高,短期內作為模型能力天花板的參考價值大於日常迭代驗證工具;此外作為模擬 benchmark,其能否充分代表真實世界操作場景的多樣性仍需 sim-to-real 驗證。



### Related work

  * 與同批次的 vla-eval（arXiv:2603.13966）高度相關,VLABench 很可能是 vla-eval 所支援的 benchmark 之一;也與 VLA survey（arXiv:2604.23001）中提到的 benchmark 在長時程推理評估上的結構性缺口直接呼應。
  * 論文於 2024年12月提交、2025年10月正式發表於 ICCV,暫無法確認是否已有直接後續改進版本,建議查證作者團隊（Fudan University OpenMOSS）後續發表。
  * Related work 值得 survey 的程度高:是理解 VLA 長時程推理評測子領域的重要參考點。



### Conclusion

  * 綜合評價：VLABench 是一篇經過同行評審（ICCV 2025）、任務設計完整且針對既有 benchmark 明確缺口提出系統解法的高品質 benchmark 論文,對評測 VLA 模型的推理與泛化能力有很高參考價值。
  * 與其他重要文章的關係：與同批次的 vla-eval、VLA survey（2604.23001）構成緊密的引用/呼應關係。
  * 對 ROCm/AMD：看不出與 ROCm/AMD 有明確的直接關聯,論文聚焦於機器人操作任務的 benchmark 設計與模擬環境建構,未提及具體訓練/推論硬體平台選型；此 benchmark 涉及大規模模擬渲染,若 AMD 想驗證 GPU/ROCm 在大規模機器人模擬效能上的表現,可作為測試案例,但此為推測方向。