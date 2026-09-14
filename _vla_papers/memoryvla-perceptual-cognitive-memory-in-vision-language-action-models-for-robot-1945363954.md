---
layout: paper
title: "MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation"
section: vla
page_id: "1945363954"
permalink: /vla/memoryvla-perceptual-cognitive-memory-in-vision-language-action-models-for-robot-1945363954/
---

**Paper** : [MemoryVLA: Perceptual-Cognitive Memory in Vision-Language-Action Models for Robotic Manipulation](https://arxiv.org/abs/2508.19236)  
**Source** : arXiv (cs.RO / cs.CV), ICLR 2026  
**arXiv ID** : 2508.19236

### Abstract

本文指出機器人操作任務本質上是「非馬可夫」（non-Markovian）的，需要時間脈絡（temporal context）才能正確決策，但主流 VLA 模型通常忽略此點，導致在長時程（long-horizon）、具時間依賴性的任務上表現不佳。作者受認知科學啟發——人類倚賴工作記憶（working memory）緩衝短期表徵以進行即時控制，同時海馬迴系統保存過去經驗的逐字情節細節與語意精華以形成長期記憶——提出 MemoryVLA，一個「認知-記憶-動作」（Cognition-Memory-Action）框架。預訓練 VLM 將觀測編碼為感知與認知 token 形成工作記憶，同時一個「感知-認知記憶庫」（Perceptual-Cognitive Memory Bank）儲存從中萃取整合的低階細節與高階語意。工作記憶會從記憶庫檢索決策相關條目，與當前 token 自適應融合，並透過合併冗餘資訊來更新記憶庫。最終以這些 token 條件化一個記憶引導的擴散式動作專家（diffusion action expert），產生具時間感知能力的動作序列。

### Method

![Figure](/assets/images/1945363954_memoryvla_fig1.png) 

_Figure 1：動機示意圖。(a) 在按按鈕等任務中，操作前後的視覺狀態幾乎相同，凸顯了時序建模的必要性。(b) 人類透過雙重記憶系統處理操作任務：知覺記憶(perceptual memory)與認知記憶(cognitive memory)協同運作。_

![Figure](/assets/images/1945363954_memoryvla_fig2.png) 

_Figure 2：MemoryVLA 整體架構。RGB 觀測與語言指令由 7B VLM 編碼為知覺(perceptual)與認知(cognitive)tokens，組成短期工作記憶(working memory)，並透過感知-認知記憶庫(PCMB)進行檢索、融合與固化，最終驅動動作解碼。_

  * 要解決的問題：機器人操作任務本質為非馬可夫，僅依賴當前觀測的 VLA 模型難以應對長時程、需要跨時間步驟推理依賴的任務。
  * Main method：提出 Cognition-Memory-Action 三段式框架：
    * Cognition：預訓練 VLM 將當前觀測編碼為「感知 token」（perceptual tokens，低階視覺細節）與「認知 token」（cognitive tokens，高階語意），兩者共同構成工作記憶（working memory）。
    * Memory：一個 Perceptual-Cognitive Memory Bank 儲存從過去互動中整合（consolidate）出的低階細節與高階語意；工作記憶會查詢此記憶庫，檢索與當前決策相關的條目，並與當前 token 自適應融合；記憶庫本身透過合併冗餘項目來持續更新。
    * Action：以融合後的 token 條件化一個「記憶條件化的擴散動作專家」（memory-conditioned diffusion action expert），輸出具時間一致性的動作序列。
  * 和以往方式的差異：相較於主流 VLA 只以當前觀測作決策，本方法明確模仿人類「工作記憶＋長期情節/語意記憶」的雙軌認知架構，並將記憶檢索與融合機制整合進動作生成流程，而非僅將歷史幀簡單拼接進輸入視窗。
  * 重要方法設計描述：架構可想像為三層管線——輸入影像/語言經 VLM 產出兩類 token；這些 token 一邊構成即時工作記憶，一邊查詢外部記憶庫做跨時間檢索；檢索到的記憶與當前工作記憶融合後，經冗餘合併更新回記憶庫，形成一個持續演化的記憶系統；最後這組時間感知 token 進入擴散模型解碼出動作序列。



### Result

  * 在 150 多個模擬與真實世界任務、三種機器人平台上評測。模擬基準：SimplerEnv-Bridge 71.9%、Fractal 72.7%、LIBERO-5 96.5%、Mikasa-Robo 41.2% 成功率，皆超越 state-of-the-art 基線 CogACT 與 pi-0，在 Bridge 上領先 +14.6、在 Mikasa-Robo 上領先 +11.8。
  * 在 12 個涵蓋一般技能與長時程時間依賴的真實世界任務上，達成 84.0% 成功率，其中長時程任務相較於最強基線提升 +26。
  * 是否公正：摘要中比較對象明確（CogACT、pi-0），數字具體且來自多個標準基準（SimplerEnv、LIBERO、Mikasa-Robo），可信度較高；但論文為原作者自評，仍需查證其他論文（如後續 MemoryVLA++ 或 EventVLA）是否對這些數字有不同復現結果或提出質疑。



### Limitation

  * 摘要中未明確自陳限制，需要查證全文中是否有討論記憶庫規模成長、檢索延遲、或記憶融合準確度等潛在瓶頸。
  * 從其後續論文 MemoryVLA++（同作者群，2026年6月）可推知，MemoryVLA 本身僅處理「記憶」（對過去的回顧），缺乏「想像」（對未來狀態的預測），此為 MemoryVLA++ 明確指出並補強的缺口，也側面反映 MemoryVLA 本身在需要前瞻規劃的任務上可能仍有限制。



### Related work

  * 已知有更新的後續研究：同作者群於 2026 年 6 月發表 MemoryVLA++（arXiv:2606.09827），在 MemoryVLA 的記憶機制基礎上加入「世界模型式想像」（world model imagination）機制，屬於直接延伸關係，值得優先追蹤。
  * 判斷此系列（MemoryVLA → MemoryVLA++）代表了 VLA 記憶機制研究的一條主線，值得列入 survey 重點閱讀。



### Conclusion

  * 綜合評價：本文提出了認知科學啟發、結構清晰的記憶框架，並在多個公開基準與真實機器人上取得顯著且具體的效能提升（尤其是長時程任務 +26 的提升相當可觀），是 VLA 記憶研究方向中重要的代表作，值得參考。
  * 與其他重要文章的關係：本文明確以 CogACT、pi-0 作為比較基線（挑戰/超越對象），且本身後續被同作者群以 MemoryVLA++ 延伸（加入世界模型想像能力）；EventVLA、LaMem-VLA 等論文也在摘要中隱含將此類「記憶庫」方法列為比較對象（例如 EventVLA 提及既有記憶增強方法的資訊瓶頸問題）。
  * ROCm/AMD 待補強部分：摘要未提及任何特定硬體或框架資訊，論文的擴散式動作專家與 VLM 編碼器可能有相當的推論延遲需求，這類記憶庫檢索與融合機制在真實機器人上需要低延遲執行；若要在 ROCm 平台部署，可能需要評估擴散模型迭代解碼與記憶檢索操作的算子支援與優化程度，但摘要本身未提供足夠資訊佐證，此為推測而非論文明確結論。