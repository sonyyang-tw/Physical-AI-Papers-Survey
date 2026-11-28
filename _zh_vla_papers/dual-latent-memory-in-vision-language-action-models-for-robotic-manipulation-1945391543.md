---
layout: paper
title: "Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation"
section: vla
page_id: "1945391543"
permalink: /zh/vla/dual-latent-memory-in-vision-language-action-models-for-robotic-manipulation-1945391543/
---

**Paper** : [Dual Latent Memory in Vision-Language-Action Models for Robotic Manipulation (LaMem-VLA)](https://arxiv.org/abs/2607.07608)  
**Source** : arXiv (cs.RO / cs.CV)  
**arXiv ID** : 2607.07608

### Abstract

本文指出主流 VLA 模型在馬可夫假設下，主要依賴當前觀測預測動作，因而難以應對長時程、具時間依賴性的任務。既有記憶增強 VLA 方法要嘛擴大觀測視窗，要嘛從記憶庫檢索歷史作為策略端的輔助脈絡，但這些記憶始終存在於 VLA 推理的原生潛在嵌入空間之外，使歷史經驗無法流暢地與多模態推理及動作生成交織融合。為此，作者提出 LaMem-VLA，一個「潛在記憶原生」（latent-memory-native）框架，將歷史經驗重建為潛在記憶 token，直接與 VLA 推理交織。其核心包含四個協同元件：(i) curator（策展者）將歷史經驗組織成短期與長期兩個互補的記憶庫；(ii) seeker（探尋者）使用多模態認知查詢兩個記憶庫，檢索與脈絡相關的證據；(iii) condenser（凝縮者）將檢索到的證據重建為緊湊的短期與長期潛在記憶 token；(iv) weaver（編織者）將這些記憶 token 與當前觀測、指令一起注入成一個連續的嵌入序列。透過在同一連續潛在空間中表徵、檢索、消費歷史經驗，LaMem-VLA 使記憶能在有界脈絡下直接參與 VLA 推理並引導動作生成。作者在 SimplerEnv 與 LIBERO 上進行大量實驗，證實 LaMem-VLA 的優越性。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945391543_lamemvla_fig1.png) 

_Figure 1：記憶增強型 VLA 模型的範式比較。與先前將歷史經驗存於輔助記憶庫、再透過檢索方式消費記憶的作法不同，圖中對比了不同記憶機制的設計理念與資訊流動方式。_

![Figure]({{ site.baseurl }}/assets/images/1945391543_lamemvla_fig2.png) 

_Figure 2：LaMem-VLA 框架架構。給定指令與當前觀測，視覺-語言編碼器首先將輸入編碼為多模態表徵，再透過雙尺度潛在記憶(dual-scale latent memory)機制進行記憶的寫入、檢索與融合，驅動動作生成。_

  * 要解決的問題：既有記憶增強 VLA 方法將記憶視為「策略端外部輔助脈絡」，記憶存在於 VLA 原生潛在嵌入空間之外，導致歷史經驗無法與多模態推理及動作生成自然交織融合，限制了記憶的有效利用。
  * Main method：提出「潛在記憶原生」框架 LaMem-VLA，由四個協同元件組成：
    * Curator（策展者）：將歷史經驗組織成兩個互補的記憶庫——短期記憶庫（short-term vault）與長期記憶庫（long-term vault）。
    * Seeker（探尋者）：利用當前多模態認知（multimodal cognition）查詢這兩個記憶庫，檢索與當前脈絡相關的證據。
    * Condenser（凝縮者）：將檢索到的證據重建、壓縮為緊湊的短期與長期「潛在記憶 token」。
    * Weaver（編織者）：將這些潛在記憶 token 與當前觀測、指令一起，編織成單一連續嵌入序列，直接餵入 VLA 的推理流程。
  * 和以往方式的差異：核心差異在於記憶的「表徵空間」——本方法將記憶表徵、檢索、消費全程都保持在與 VLA 推理相同的連續潛在空間中（"latent-memory-native"），而非像既有方法把記憶當作外部模組（如文字記憶、獨立記憶庫）事後拼接進策略輸入,因此能讓記憶在有界脈絡（bounded context）下直接、流暢地參與推理與動作生成過程,而非僅作為附加脈絡。
  * 重要方法設計描述：可將此架構想像成一條「記憶生產線」——策展者先把原始歷史經驗分裝進短期/長期兩個倉庫；探尋者依據當下任務需求主動去倉庫裡查找相關證據；凝縮者把找到的證據壓縮成精簡的潛在向量（而非保留原始高維度資料）；最後編織者將這些壓縮後的記憶向量與當前畫面、指令的嵌入表徵縫合成一條連續序列，直接送入 VLA 的多模態推理主幹，使記憶與當前推理處於同一運算空間、無縫銜接。



### Result

  * 在 SimplerEnv 與 LIBERO 兩個公開基準上進行大量實驗，摘要中陳述「證實了 LaMem-VLA 的優越性」（demonstrate the superiority），但未在摘要中提供具體量化數字（如成功率百分比、相對提升幅度）。
  * 是否公正：由於摘要未附上具體實驗數據，無法在此判斷其效果的具體量級與說服力；需要查證全文以取得詳細的成功率、消融實驗結果，並確認與哪些基線（是否包含 MemoryVLA、EventVLA 等同期記憶增強 VLA）比較。



### Limitation

  * 摘要未明確自陳限制。從架構設計推測，四段式流水線（curator → seeker → condenser → weaver）涉及多次檢索與壓縮操作，可能帶來額外的推論延遲；同時「短期/長期記憶庫」的容量管理與更新策略（何時淘汰舊記憶）在摘要中未說明，需查證全文。
  * 摘要未提供具體量化結果也是本篇在透明度上的一項限制，難以獨立評估其效能與穩健性。



### Related work

  * 摘要中明確以「既有記憶增強 VLA 方法將記憶置於原生潛在空間之外」作為批評既有方法（可能包括 Explicit Language Memory 的顯式文字記憶,以及部分將記憶當作外部檢索模組的方法）的出發點,隱含挑戰/對照關係，但未點名具體論文。
  * 判斷此文與 MemoryVLA/MemoryVLA++（同樣使用潛在 token 形式的記憶，但強調「感知-認知」雙軌而非「短期-長期」雙軌）、EventVLA（強調稀疏事件記憶而非連續潛在記憶）同屬 2026 年 VLA 潛在記憶研究群體，彼此設計理念相近但細節路線不同，值得在 survey 中並列比較，判斷其 related work 具有中高度的 survey 價值。



### Conclusion

  * 綜合評價：LaMem-VLA 提出的「記憶全程留在同一潛在空間」的設計理念具有一定的方法論吸引力（避免記憶與推理之間的表徵鴻溝），四段式流水線（curator/seeker/condenser/weaver）架構清晰、分工明確，但由於摘要缺乏具體量化結果，實際效能優劣仍待查證全文與後續社群復現確認。
  * 與其他重要文章的關係：本文與 MemoryVLA/MemoryVLA++（感知-認知記憶庫）、EventVLA（稀疏事件記憶）、Explicit Language Memory（顯式文字記憶）共同構成 2026 年 VLA 記憶機制研究的多元路線圖，彼此在「記憶表徵形式」（潛在向量 vs. 文字）與「記憶組織方式」（短期/長期 vs. 感知/認知 vs. 稀疏事件）上各有取捨，適合作為同一 survey 主題下並列比較的一組論文。
  * ROCm/AMD 待補強部分：摘要未提及任何硬體平台資訊。此方法涉及多階段記憶檢索與潛在向量壓縮操作，這類非標準的注意力/檢索運算在不同硬體平台上的算子支援程度可能有差異，但論文本身未提供任何實測數據或硬體討論，因此看不出與 ROCm/AMD 的明確關聯，此為推測，非論文結論。