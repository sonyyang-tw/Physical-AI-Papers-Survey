---
layout: paper
title: "Helix: A Vision-Language-Action Model for Generalist Humanoid Control"
section: vla
page_id: "1945393112"
permalink: /Physical-AI-Papers-Survey/vla/helix-a-vision-language-action-model-for-generalist-humanoid-control-1945393112/
---

**Paper** : [Helix: A Vision-Language-Action Model for Generalist Humanoid Control](https://www.figure.ai/news/helix)  
**Source** : Figure AI 官方技術部落格(非正式 arXiv 論文,Figure AI 未發表對應的 arXiv 學術論文)  
**arXiv ID** : 無(此為公司技術部落格發表,無 arXiv ID)

### Abstract

Helix 是 Figure AI 發表的一種「System 1、System 2」式 VLA 模型,號稱首創能對整個人形機器人上半身(包含手腕、軀幹、頭部與各手指)進行高速率、靈巧控制。其核心創新針對先前方法的根本取捨進行突破:過去 VLM 骨幹雖具通用性但速度不足,而機器人視覺運動策略雖速度快但通用性不足。Helix 號稱是首個能對整個人形機器人上半身輸出高速率連續控制的 VLA,以 200Hz 協調 35 自由度(DoF)的動作空間,涵蓋從個別手指動作到末端執行器軌跡、頭部注視、軀幹姿態的所有層面。Helix 也號稱是首個能同時在兩台機器人上運作的 VLA,使兩台機器人能共同解決一項共享的長時程操作任務,處理它們從未見過的物品。有別於先前方法,Helix 使用單一組神經網路權重來學習所有行為——包括撿取放置物品、使用抽屜與冰箱、跨機器人互動——完全不需針對任務進行微調。

### Method

![Figure](/Physical-AI-Papers-Survey/assets/images/1945393112_helix_fig1.png) 

_Figure 1: Scaling curves for different approaches to acquiring new robot skills — heuristic manipulation scales with PhD engineering time, imitation learning scales with collected data, Helix enables new skills specified on the fly via language (Helix 官網未提供獨立的 System 1/System 2 架構示意圖，僅以文字描述架構)_

  * 要解決的問題:先前的 VLA 方法面臨一個根本取捨——大型 VLM 骨幹具備通用的語意理解能力但推論速度不足以支撐高頻靈巧控制;而專門的視覺運動策略(visuomotor policy)速度雖快,卻缺乏語意通用性。Helix 試圖同時解決「通用性」與「高速率控制」這兩個看似衝突的需求。
  * 主要方法:採用「System 1、System 2」雙系統設計——System 2 是一個 70 億參數的多模態語言模型,以 7-9Hz 運作,擔任分析型的「大腦」角色,負責語意理解與高層決策;System 1 是一個快速的視覺運動策略,負責高頻(200Hz)、35 自由度的連續控制輸出。
  * 與以往方式的差異:Helix 並未採用客製化的全新架構,而是刻意使用標準架構組件——System 2 使用開源、開放權重的 VLM,System 1 使用簡單的基於 transformer 的視覺運動策略。其創新之處在於系統整合設計(單一權重集合學習所有行為、跨機器人協作、全上半身高頻控制),而非模型架構本身的創新。訓練資料為約 500 小時的多機器人、多操作員遠端teleoperation 資料,並使用自動標註 VLM 為資料生成事後(hindsight)指令標籤以支援語言條件化。
  * 重要方法設計描述:System 2(7B 多模態 LLM,7-9Hz)接收視覺與語言輸入,產出語意層級的表徵或指令,傳遞給 System 1;System 1(transformer-based visuomotor policy)以 200Hz 高頻率輸出 35 自由度動作(涵蓋手腕、軀幹、頭部、各手指);模型使用單一組權重涵蓋所有已學會的行為(無需任務專屬微調);Helix 完全在低功耗嵌入式 GPU 上運行,無需雲端連線,適合商業部署;後續的「Helix Logistics」更新加入了隱式立體視覺(implicit stereo vision,提供深度感知運動精度)與多尺度視覺表徵(同時捕捉細節與場景層級理解)。



### Result

  * 主要增強:Helix 號稱是首個能對人形機器人整個上半身(35 自由度)進行 200Hz 高頻連續控制的 VLA;首個能讓兩台機器人同時運作、協作完成共享長時程任務的 VLA;並且完全在嵌入式低功耗 GPU 上即時運行,無需任務專屬微調即可執行撿取放置、使用抽屜/冰箱等多樣行為。
  * 是否公正:由於這是公司自家部落格發表(非經同行評審的學術論文),缺乏獨立第三方的量化評測數據(如成功率百分比、與其他模型的直接數值比較),其宣稱的「首創」與效能描述均來自 Figure AI 官方說法,尚無法比對其他論文的比較數據,公正性有限,需要查證是否有第三方或學術評測驗證這些說法。



### Limitation

  * 由於這不是經同行評審的學術論文,官方部落格中未明確列出限制章節或失敗案例分析。從公開資訊可推測的限制:(1) 缺乏公開的量化基準測試數據(如標準機器人操作 benchmark 上的成功率),難以與 OpenVLA、π0、GR00T N1 等有正式論文與量化評測的模型進行公正比較;(2) 訓練資料規模(約 500 小時遠端teleoperation 資料)相對於 OpenVLA(970k 筆示範)、π0(涵蓋 7 種本體 68 種任務)等經過同行評審論文詳述的資料規模,是否足夠支撐更廣泛的任務泛化,缺乏公開驗證;(3) 作為商業產品的一部分,其技術細節(如具體模型架構參數、訓練方法細節)的揭露程度不及學術論文完整,獨立研究者難以復現或深入分析。



### Related work

  * Helix 的「System 1 / System 2」雙系統設計理念與 NVIDIA GR00T N1(2503.14734)的雙系統(VLM + 擴散變換器)架構高度相似,兩者都採用「慢速語意理解 + 快速動作生成」的分工原則,值得對照比較兩者的具體實現差異。
  * 後續 Figure AI 發布了「Helix Logistics」更新部落格,加入隱式立體視覺與多尺度視覺表徵改進,顯示 Helix 仍在持續迭代中。
  * 值得 survey 的程度中等:由於缺乏正式學術論文與量化評測數據,其技術可信度與可比較性不及本次任務中其他有 arXiv 論文的模型(RT-2、OpenVLA、π0、GR00T N1),建議將其視為業界工程實踐的參考案例,而非嚴謹的學術研究對象,survey 時應以了解「業界動態」為主要目的,而非作為技術細節的可靠來源。



### Conclusion

  * 綜合評價:Helix 展示了人形機器人 VLA 在商業化部署上的一種可行工程路徑(雙系統、單一權重、嵌入式低功耗運行),對於了解業界(尤其是人形機器人新創公司)如何將 VLA 概念落地為實際產品具有參考價值;但由於缺乏同行評審與公開量化評測,其技術聲稱的嚴謹度不及本次任務中其他有正式 arXiv 論文的模型,建議謹慎看待其宣稱的「首創」與效能描述。
  * 與其他重要文章的關係:Helix 與 GR00T N1 的雙系統(System 1/System 2)設計理念相呼應,兩者都反映了「人形機器人 VLA 需要拆分語意理解與高頻動作生成」這一業界共識;與 π0、OpenVLA 等學術模型相比,Helix 更強調工程落地(單一權重覆蓋所有行為、嵌入式低功耗部署),顯示產業界與學術界在 VLA 研究上有不同的側重點(產業重視部署效率與產品化,學術界重視可解釋性與量化評測嚴謹度)。對 ROCm/AMD 而言,Helix 強調完全在嵌入式低功耗 GPU 上運行(暗示可能使用 NVIDIA Jetson 系列或類似嵌入式平台),若 AMD 有對應的嵌入式/邊緣 GPU 產品線,這類「VLA 邊緣部署」的市場趨勢值得關注,但論文(部落格)本身未提及具體使用的硬體型號或是否考慮過 AMD 平台,此為觀察到的產業趨勢而非論文明文提及的關聯。