---
layout: paper
title: "τ0-WM: A Unified Video-Action World Model for Robotic Manipulation"
section: wm
page_id: "1945767449"
permalink: /zh/wm/τ0-wm-a-unified-video-action-world-model-for-robotic-manipulation-1945767449/
---

**Paper** : [τ0-WM: A Unified Video-Action World Model for Robotic Manipulation](https://arxiv.org/abs/2606.01027)  
**Source** : arXiv / 官方技術報告(AGIBOT Finch / Shanghai Innovation Institute),項目主頁 <https://finch.agibot.com/research/tau0-wm>  
**arXiv ID** : 2606.01027

### Abstract

機器人操作需要能在實際執行前「產生可執行動作」同時「預測並評估其未來後果」的模型。本文提出τ0-World Model(τ0-WM),一個統一的視頻-動作世界模型,將政策學習(policy learning)、視頻預測(video prediction)、動作評估(action evaluation)整合在單一的未來預測框架內。τ0-WM建立在共享的視頻擴散骨幹(video diffusion backbone)上,提供兩個互補介面:第一,視頻動作模型(video action model)根據多視角觀測、語言指令與機器人狀態,聯合預測未來視覺潛變量(latent)與連續動作片段(action chunk);第二,動作條件化的視頻模擬器(action-conditioned video simulator)將候選動作片段rollout成多視角未來畫面,並預測密集的任務進度分數。模型使用約27,300小時的真實機器人遙操作、UMI風格互動、第一人稱人類影片,以及rollout/失敗軌跡等資料,透過模態專屬的監督遮罩(modality-specific supervision mask)訓練。推論時,τ0-WM使用測試時計算(test-time computation)採樣候選動作、以re-denoising一致性評分排序,並對低品質候選調用模擬器進行修正。在具挑戰性的長時序與精細機器人操作任務上,τ0-WM相較於其他相關baseline展現出更優異的表現。

### Method

![Figure]({{ site.baseurl }}/assets/images/1945767449_tau0wm_fig1.png) 

_Fig. 1: Overview of the τ0-WM framework — jointly training a Video Action Model and Action-Conditioned Video Simulator for test-time action selection._

![Figure]({{ site.baseurl }}/assets/images/1945767449_tau0wm_fig2.png) 

_Fig. 2: Architecture of τ0-WM — Video Action Model (VAM) as policy interface and Action-Conditioned Video Simulator (ACVS) as evaluation interface._

  * 要解決的問題:機器人操作模型往往將「產生動作」與「評估/模擬動作後果」分開處理,難以在單一框架內同時兼顧策略學習的效率與世界模型模擬的保真度,尤其在長時序、精細操作任務上容易失敗。
  * Main method:τ0-WM以共享的視頻擴散backbone同時支援兩種功能——(1)視頻動作模型:從多視角觀測、語言指令、機器人狀態聯合預測未來視覺潛變量與連續動作片段;(2)動作條件化的視頻模擬器:將候選動作序列rollout為多視角未來畫面並評分任務進度。推論時採用「Propose–Evaluate–Revise」(提議-評估-修正)循環:先取樣多個動作片段候選,以re-denoising一致性分數排序;若無候選評分理想,則進一步用世界模型模擬未來畫面,挑選最有希望的rollout結果,並以此條件化第二次動作預測,形成測試時的提議-評估-修正循環。
  * 和以往方式的差異:與過去將video prediction、action policy、evaluation分開訓練或視為獨立模組的方法不同,τ0-WM用單一共享的視頻擴散backbone統一這三個功能,並引入測試時計算(而非僅依賴訓練時的能力)來動態改善動作選擇品質,這是相對於單純「生成動作後直接執行」方法的關鍵差異。
  * 重要方法設計描述:訓練資料包含三個來源——17.8K小時的真實機器人遙操作(AGIBOT-G01、ARX機械臂、雙臂Franka系統)、6.5K小時經篩選的開源UMI風格示範、3.0K小時開源第一人稱人類互動影片,共約27.3K小時,並以模態專屬遮罩區分不同資料型態的監督訊號。推論流程可想像為:模型先像一般VLA政策一樣提出多個動作候選,再用同一個視頻擴散backbone「想像」執行這些動作後的多視角未來畫面,並對這些想像結果評分,篩掉不佳的候選或用模擬結果修正下一輪的動作預測,如此反覆直到動作品質達標或達到計算預算上限。



### Result

  * 在具挑戰性的長時序及精細機器人操作任務上,τ0-WM相較於相關baseline取得最佳的平均成功率。
  * 在四個訓練資料未出現過的任務(unseen tasks)中,τ0-WM在多數對精度要求高的任務上表現最強,但「Faucet」(水龍頭)任務對所有方法都仍然困難,顯示該任務尚未被充分解決(未飽和)。
  * 摘要與搜尋結果未提供與Ctrl-World、WEAVER等其他world model的直接量化對比數字(如成功率百分比差異),需要查證其他論文的比較數據以確認相對優劣。



### Limitation

  * 從公開資訊看,論文提及Faucet任務對所有方法都困難,顯示系統在某些高精度/高摩擦力接觸任務上仍有明顯弱項,這可視為作者間接自陳的限制之一。
  * 摘要與搜尋結果未提供完整的Limitation章節內容,需要查證全文以確認作者是否有更詳細討論訓練資料偏差、跨機器人形態泛化能力、或測試時計算(test-time compute)帶來的延遲成本等限制。
  * 從方法設計推論的潛在弱項:測試時的「提議-評估-修正」循環雖然可以提升動作品質,但代價是額外的推論運算量與延遲,對於即時性要求高的實際部署場景可能構成挑戰(全文未明確量化此延遲成本)。



### Related work

  * 同團隊(AGIBOT Finch / Shanghai Innovation Institute)後續發表了τ0-VLA(arXiv:2608.16885),是一個分層式(hierarchical)機器人基礎模型,以世界模型導引測試時計算來處理長時序機器人操作,可視為τ0-WM概念的進一步延伸,值得一併追蹤。
  * 與Ctrl-World、WEAVER同屬「用world model評估/改進機器人操作政策」的研究方向,可互相比較架構設計(如統一backbone vs. 分離模組、記憶檢索機制等)。
  * 值得survey的程度:中高。這是一篇資料規模與工程整合度都相當高的技術報告,且有明確的後續延伸工作(τ0-VLA),值得追蹤此系列的演進。



### Conclusion

  * 整體評價:值得參考,尤其是其「統一視頻-動作世界模型」與「測試時提議-評估-修正循環」的設計思路,對於想要在單一框架內同時處理策略生成與模擬評估的團隊有參考價值。但由於資料來源為官方部落格/技術報告與非正式arXiv頁面(2606.01027,注意此為2026年5月提交而非傳統期刊發表),其同儕評審狀態需另行確認。
  * 與其他重要文章的關係:與Ctrl-World、WEAVER同屬機器人操作world model的研究路線,並延伸出τ0-VLA。它與Ctrl-World的差異在於,τ0-WM更強調「統一單一backbone同時做策略與模擬」,而非像Ctrl-World將world model作為獨立的評估/資料生成工具。
  * ROCm/AMD相關性:論文內容聚焦於模型架構、訓練資料規模與機器人任務評測,未提及所使用的計算硬體平台或ROCm相關資訊。從現有資訊看不出與ROCm/AMD有明確關聯;若要評估此類27.3K小時級別大規模影片擴散訓練在AMD硬體上的可行性,需要查證全文的訓練基礎設施章節(若有)。