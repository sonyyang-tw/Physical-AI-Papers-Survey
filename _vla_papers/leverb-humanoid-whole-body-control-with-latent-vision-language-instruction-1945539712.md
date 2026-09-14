---
layout: paper
title: "LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction"
section: vla
page_id: "1945539712"
permalink: /vla/leverb-humanoid-whole-body-control-with-latent-vision-language-instruction-1945539712/
---

**Paper** : [LeVERB: Humanoid Whole-Body Control with Latent Vision-Language Instruction](https://arxiv.org/abs/2506.13751)  
**Source** : arXiv (cs.RO)  
**arXiv ID** : 2506.13751

### Abstract

LeVERB 是第一個針對人形機器人全身控制（Whole-Body Control, WBC）設計的視覺語言潛在指令框架。現有的 VLA 系統多半假設有一個精確的低階控制器與人工設計的動作「詞彙」（例如末端執行器姿態或根部速度），這使得它們只能處理準靜態（quasi-static）任務，無法完成人形機器人所需的敏捷全身動作。作者提出兩項貢獻：（1）第一個 sim-to-real、支援視覺語言、閉迴路的人形 WBC benchmark，涵蓋 10 大類超過 150 項任務；（2）LeVERB 框架本身，一個階層式的「潛在動作詞彙」系統，高階視覺語言策略從合成渲染的人類動作示範中學習潛在動作詞彙，低階則由強化學習訓練的 WBC 策略將這些潛在指令轉為動力學層級的控制指令。

### Method

![Figure](/assets/images/1945539712_leverb_fig1.png) 

_Figure 1: 論文貢獻總覽 ——上方為照片級擬真且動力學精確的人形視覺語言全身控制 benchmark；中間為僅以合成資料訓練、於真實世界零樣本部署的雙程序 VLA 模型；下方為解耦視覺語言與動力學層級動作處理的模型架構總覽。_

![Figure](/assets/images/1945539712_leverb_fig2.png) 

_Figure 2: 資料蒐集與訓練管線細節。步驟一：在 IsaacSim 中收集重定向動作的合成照片級資料集並標註文字指令；步驟二：以動作軌跡重建任務訓練 LeVERB-VL，得到正規化的潛在動詞詞彙並為資料集中每段軌跡快取潛在動詞；步驟三：以此潛在動詞條件化 LeVERB-A，該模型由教師追蹤策略以 DAgger 蒸餾而成。_

  * **要解決的問題** ：既有 VLA 假設精確、手工設計的動作詞彙（如末端執行器姿態），僅適用於準靜態操作任務，無法涵蓋人形機器人所需的高動態全身控制（例如行走、跌倒恢復、全身操作與移動的協調）。
  * **主要方法** ：LeVERB 採雙層（System 2 / System 1）階層架構。
    * 高層（System 2）：一個視覺語言策略，以 CVAE（條件變分自編碼器）架構學習一個結構化的「潛在動作詞彙」空間，將視覺與語言輸入對齊到一個統一的潛在動作分布，而非依賴人工定義的動作原語。
    * 低層（System 1）：一個以強化學習訓練的全身控制（WBC）反應式控制器，接收高層輸出的潛在「動詞」，轉換為機器人動力學層級的具體控制命令。
  * **與以往方式的差異** ：以往的分層 VLA 通常在高低層之間使用人工設計、離散且語意受限的動作介面（如末端執行器目標點），而 LeVERB 用學習到的連續潛在空間取代這個介面，使得動作詞彙本身是從資料中學來的，能表達更豐富、更動態的全身行為。
  * **重要設計** ：為了解決機器人專屬視覺資料稀缺的問題，作者建立了一套資料合成管線：收集多樣的人類動作、將其重定向（retarget）到人形機器人身上，並在隨機化場景中做照片級渲染，再用 VLM 標註語意相似的語言指令，從而產生「配對的機器人專屬影片-語言」資料來訓練高層 VLA。



### Result

  * 在自建 benchmark 上，LeVERB 在簡單視覺導航任務上可達到 80% 零樣本成功率，整體平均成功率 58.5%，比單純的階層式 VLA 實作高出 7.8 倍。
  * 團隊也在真實的 Unitree G1 人形機器人上展示了動力學層級的零樣本 sim-to-real 遷移。
  * 是否公正：由於 benchmark 是作者自建的（尚無其他獨立第三方在同一 benchmark 上大規模覆現數據），對比基準主要是「naive hierarchical VLA implementation」，屬於作者自行實作的 baseline，此比較是否具代表性需要查證其他論文或後續 benchmark 結果加以驗證。



### Limitation

  * 論文本身：目前發現的細節顯示其高度依賴合成資料管線（人類動作重定向與渲染），真實資料與合成資料之間可能存在 domain gap，摘要未明確提及作者如何量化這個 gap。
  * 從結果來看，58.5% 的整體成功率顯示在多數（非簡單導航）任務類別中仍有相當大的失敗率，說明複雜全身操作任務對此框架仍具挑戰性；需要進一步查證全文以了解具體失敗模式（例如哪些任務類別表現最差）。



### Related work

  * 已知有後續研究直接建立在 LeVERB 的潛在動作概念之上：WholeBodyVLA（arXiv 2512.11047，ICLR 2026），標題為「Towards Unified Latent VLA for Whole-Body Loco-Manipulation Control」，延伸至統一的全身移動-操作（loco-manipulation）控制。
  * 值得 survey 的程度：中高。此領域（人形全身 VLA）發展快速，且已有直接後續工作，建議追蹤 WholeBodyVLA 及其他基於潛在動作詞彙的全身控制研究。



### Conclusion

  * 綜合評價：值得參考。LeVERB 提出的「潛在動作詞彙」取代手工動作介面的想法，是解決人形機器人全身控制與 VLA 結合的一個具體且有 sim-to-real 驗證的方案，且已產生後續研究（WholeBodyVLA），顯示其方法論具有影響力。
  * 與其他論文關係：LeVERB 挑戰了傳統階層式 VLA 對精確低階控制器與人工動作詞彙的假設；其後續作 WholeBodyVLA 進一步延伸此概念。
  * ROCm/AMD 關聯：從摘要內容看不出與 ROCm/AMD 有明確關聯，論文未提及具體訓練/推論硬體平台或框架細節；如需評估在 AMD 硬體上的訓練/部署可行性，需要查證全文的模型規模、訓練基礎設施與延遲需求等資訊。