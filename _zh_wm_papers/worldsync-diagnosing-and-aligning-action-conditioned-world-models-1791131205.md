---
layout: paper
title: "Do Robotic World Models Really Follow Actions? Diagnosing and Aligning Action-Conditioned Generation for Policy Learning"
section: wm
page_id: "1791131205"
permalink: /zh/wm/worldsync-diagnosing-and-aligning-action-conditioned-world-models-1791131205/
---

### Abstract

動作條件化世界模型(Action-Conditioned World Model, AC-WM)正日益被當作學習型模擬器,用於 policy 評測與後訓練改進,但其有效性建立在一個從未被嚴格驗證的假設之上:生成的未來影格會忠實反映「任意合法動作」,而不只是示範資料中出現過的動作。既有 benchmark 通常只用專家示範的動作做評測,這與一個學習中的 policy 在線上評測/改進過程中實際會查詢到的狀態-動作分佈必然存在落差(類似 DAgger 問題中的分佈偏移)。為填補這個缺口,作者提出 WorldEcho,透過視覺完整性與 SE(3) 軌跡對齊,在更廣泛的動作分佈上探測「動作跟隨」能力。診斷結果顯示,現有世界模型能合理執行專家動作,但面對多樣化的非專家軌跡時會出現困難,要嘛忽略指令動作、要嘛生成視覺上無效的 rollout。作者進一步提出 WorldSync,沿著三個互補的軸線強化動作跟隨能力:分佈覆蓋廣度、表徵層級的動態 grounding、以及介入效果對齊。WorldSync 擴大了動作後果的訓練分佈,透過一個 Action-Forcing Expert 將中間影片表徵 grounding 到動作引致的機器人動態上,並讓模型在動作介入下的預測變化與真實未來的對應變化對齊。在 RoboTwin benchmark 與真實機器人任務上的實驗顯示,WorldSync 改善了 WorldEcho 各項指標,也是更可靠的迭代式 policy 改進模擬器,讓 policy 取得更高的成功率。本論文由北京大學多媒體資訊處理全國重點實驗室、北京人形機器人創新中心,與紐約大學、電子科技大學、南洋理工大學、香港中文大學共同作者於 2026 年 8 月 25 日發佈於 arXiv。

### Method

- **要解決的問題**:AC-WM 被期望能作為真實世界互動的廉價替代品,用於評測 policy 或透過想像 rollout 做後訓練改進。但這個用途隱含一個關鍵假設——世界模型生成的未來必須忠實跟隨「任意合法的」動作指令,而不只是在訓練時見過的專家動作分佈內表現良好。現有的 AC-WM 評測 benchmark 幾乎都只用專家示範的動作重播來測試,這種評測方式完全無法揭露模型在面對一個正在被評測或改進的 policy 實際會查詢到的、偏離專家分佈的動作時會如何表現。這個问题类似模仿學習中的 DAgger 分佈偏移問題——policy 在訓練階段只見過專家軌跡附近的狀態,但部署/評測時會進入專家從未到過的狀態-動作組合,而如果用來評測 policy 的世界模型本身也只在專家分佈內可靠,整個評測/改進迴圈的可信度就會崩潰。

- **Main method**:本論文分成「診斷」與「改進」兩部分。**診斷部分**:作者先在 NVIDIA Cosmos-Predict2.5 上以 RoboTwin 專家示範做微調,發現模型能很好地重播專家軌跡,但面對非專家動作查詢時出現兩種失效模式:(1) 視覺崩潰——機械臂變形、夾爪消失、畫面品質劣化;(2) 看似合理但實際錯誤的動作——影片在視覺上仍然合法,但忽略或錯配了指令動作(一種「樂觀偏誤」)。**WorldEcho(診斷 benchmark)**:將 AC-WM 形式化為 p_θ(I_{1:H} | o_0, c, a_{1:H}),即根據初始觀測 o_0、指令 c、動作序列 a_{1:H} 生成未來多視角影片;ground truth 透過在 RoboTwin 模擬器中重播相同動作序列取得。設計了 5 種動作查詢類別,依序遞減對「專家狀態-動作聯合分佈」的依賴:(1) Demonstrated Action(專家動作,分佈內基準)、(2) Cross-State Replay(專家動作但套用於不同狀態——測試狀態條件化效果)、(3) Local Perturbation(專家動作的有界擾動)、(4) Policy Rollout(來自一個已學習 policy 的動作,反映真實評測/改進場景下的狀況)、(5) Feasible-Space Sampling(廣泛的合法動作抽樣,最少依賴專家分佈)。所有非專家查詢都經過可行性過濾,並在 RoboTwin 中重播以取得動作對應的 ground truth。評測指標包含:**視覺完整性閘門 G_vis**(四項二元檢查的合取——以 MUSIQ 分數門檻判斷影像品質、以幀插值一致性門檻判斷動作平滑度、以 SAM 影片追蹤判斷末端執行器可見性、以 Qwen 系 VLM 判斷手臂是否模糊/斷裂/消失——只有四項全部通過才算有效 rollout);**SE(3) 軌跡對齊**(抽取每幀左右夾爪的三維位置 p∈R³ 與姿態 R∈SO(3),定義結合加權位置 L2 距離與 SO(3) 測地線旋轉距離(透過 R1ᵀR2 跡的反餘弦)的姿態差異量 d_e(i,j),再以姿態感知的 Normalized Dynamic Time Warping 對齊生成軌跡與 ground truth 軌跡以處理時間錯位,得到 D_NDTW);**完整性閘門加權誤差 S_n**(每筆查詢的分數在視覺閘門通過時等於 D_NDTW,未通過時則為固定懲罰值 κ,將視覺失效與軌跡失效兩種失敗模式整合為單一聚合指標,先在任務內、再跨 50 個 RoboTwin 任務做巨集平均)。**WorldSync(改進方法)**:針對三個互補軸線設計訓練配方——(1) **動作覆蓋擴增**:混合模擬專家軌跡、非專家軌跡(擾動/跨狀態/policy rollout/可行空間抽樣)與少量真實機器人目標域資料,全部以共享動作空間(機器人底座座標系下的相對笛卡爾末端執行器姿態位移)表示,在保留真實域視覺保真度的同時,跨模擬與真實遷移動作跟隨能力。(2) **Action-Forcing Expert(AFE)**:一個輔助頭,以軌跡查詢 token 逐步交叉注意中間影片區塊特徵,並解碼預測的未來末端執行器 SE(3) 軌跡;以 L_AFE(預測與 ground truth 姿態表示 ρ(·) 之間在整個 horizon 上的均方誤差)訓練。AFE 將中間影片特徵 grounding 到動作引致的機器人動態上,但推論時會被丟棄(僅作為訓練期特徵層級正則化器)。(3) **介入效果(IE)監督**:利用共享相同觀測/指令/噪聲、但動作不同(A 與 B)的成對 rollout,計算預測差異 Δ_θ = v_θ^A − v_θ^B(flow velocity 差異)與 ground truth 差異 Δ* = x_0^B − x_0^A(乾淨 latent 差異),最小化 L_IE = ||Δ_θ − Δ*||²,直接監督「動作改變時預測應如何相應改變」,而非僅對每筆 rollout 獨立擬合。骨幹模型以 flow matching 訓練:x_t = (1−t)x_0 + t·ε,L_FM 為標準的 flow-matching velocity 預測損失,條件於 (o_0, c, a_{1:H})。聯合目標為 L = L_FM + λ_AFE·L_AFE + λ_IE·L_IE。

- **和以往方式的差異**:與既有 AC-WM 評測方式相比,WorldEcho 最核心的突破是首次系統性地將「評測動作分佈」從單純的專家重播,擴展到涵蓋跨狀態重播、局部擾動、policy rollout、可行空間抽樣五種遞減專家依賴度的查詢類型,並搭配同時考慮視覺完整性與 SE(3) 軌跡精度的複合指標,而非既有工作常用的單一視覺品質分數或單一軌跡誤差。WorldSync 在方法設計上也與既有「單純擴大訓練資料覆蓋範圍」的直覺做法不同——它額外引入 AFE 做表徵層級的動態 grounding,以及 IE 監督做「動作改變→預測改變」的顯式配對監督,消融結果顯示三個軸線分別針對不同失效模式(動作一致性、視覺完整性、軌跡精度)提供互補貢獻,而非單一維度的重複堆疊。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖展示「診斷→改進→驗證」的整體研究流程,涵蓋 AC-WM 在專家與非專家動作查詢下的表現落差診斷、WorldEcho benchmark 的建構、以及 WorldSync 的驗證;第二張圖展示 WorldSync 架構總覽,包含動作覆蓋擴增的資料混合策略、Action-Forcing Expert 的軌跡查詢與交叉注意力機制、以及介入效果監督的成對 rollout 設計。

![Figure]({{ site.baseurl }}/assets/images/2608.24885_diagnose_pipeline.png)

_Figure 1: 診斷-改進-驗證整體研究流程——AC-WM 在專家與非專家動作查詢下的表現落差診斷、WorldEcho benchmark 建構、WorldSync 驗證_

![Figure]({{ site.baseurl }}/assets/images/2608.24885_worldsync_architecture.png)

_Figure 4: WorldSync 架構總覽——動作覆蓋擴增、Action-Forcing Expert 表徵 grounding、介入效果監督三軸線並行_

### Result

- **主要增強部分**:對 6 個以專家資料訓練的基線 AC-WM(CtrlWorld、Cosmos-Predict2.5、Cosmos3、DreamDojo、Motus、LingBotVA)做診斷,從專家查詢切換到非專家查詢後,完整性閘門加權誤差普遍上升 0.029–0.099 m,原始 NDTW 誤差上升 0.010–0.043 m,視覺失效率上升 6.3–28.1 個百分點——證實「非專家支持落差」這個現象在不同架構間普遍存在,而非個別模型的特例。在主要的 50 任務 RoboTwin WorldEcho benchmark 上,WorldSync 取得最佳完整性閘門加權誤差(0.0661,僅次於次佳的 CtrlWorld+擴增覆蓋 0.0670)以及最佳視覺通過率(84.51%,優於次佳 Motus 的 84.34%),不過 Cosmos-Predict2.5(搭配擴增覆蓋)在單獨的原始 NDTW 指標上略低於 WorldSync(0.0127 對比 WorldSync 的 0.0223)——即 WorldSync 是在綜合權衡上勝出,而非在每一項個別指標上都領先。消融實驗(4 項任務)顯示:單獨擴增動作覆蓋,完整性閘門加權誤差從 0.0781 降至 0.0738(原始 NDTW 從 0.0306 降至 0.0258),而視覺通過率基本持平——證實擴增覆蓋主要改善的是動作一致性本身;加入 IE 監督帶來最大的原始 NDTW 增益(單獨使用時達 0.0170,為單一改動中最佳),但略微降低視覺通過率(81.25%);單獨使用 AFE 對軌跡指標沒有幫助,但帶來最佳的視覺通過率(83.04%);完整模型(覆蓋+IE+AFE 三者合一)取得最佳的平衡後完整性閘門加權誤差 0.0695。**下游 policy 改進效益**:採用 VLAW 式迭代 policy 改進流程,在匹配的互動/rollout/訓練預算下——RoboTwin 模擬中,搭配 WorldSync 的 policy 成功率在兩輪迭代中從約 51-52% 上升至 65%(+13 個百分點),而搭配 CtrlWorld 僅達到 56-57%(+5 個百分點),落後 8-9 個百分點。在真實機器人疊杯任務上,兩者起始均為 48%;WorldSync 達到 68%(+20 個百分點),CtrlWorld 僅達 56%(+8 個百分點)——顯示更忠實的動作條件化模擬確實能在固定預算下轉化為實質更好的真實世界 policy 改進效果。

- **結果是否公正**:診斷實驗涵蓋 6 個具代表性的現有 AC-WM(包含 NVIDIA Cosmos-Predict2.5/Cosmos3 等業界級模型),且以統一的 5 類動作查詢與統一指標做比較,方法論上相對公正嚴謹。作者也誠實揭露 WorldSync 並非在每一項個別指標上都全面勝出——Cosmos-Predict2.5(擴增覆蓋版)在原始 NDTW 上實際上更低,這種不迴避「次佳」結果的呈現方式增加了可信度。下游 policy 改進實驗同時涵蓋模擬與真實機器人兩種場景,且採用匹配預算的公平比較協定,是較為嚴謹的驗證設計。

### Limitation

- **已知 limitation**:作者明確指出,WorldEcho 雖大幅拓寬了評測覆蓋範圍,但要全面探測跨越多樣具身與開放世界環境的長 horizon 互動,「仍是這個領域共同面對的挑戰,也是重要的未來研究方向」——換言之,目前的 benchmark 與方法主要在 RoboTwin(雙臂桌面操作模擬)加上有限的真實機器人任務上驗證,尚未達到開放世界、長 horizon、多具身規模的驗證層級。

- **從 result 來看的弱項**:WorldSync 在主要 benchmark 上並非所有個別指標都最優(原始 NDTW 略遜於 Cosmos-Predict2.5+擴增覆蓋版本),顯示方法在「平衡多個失效模式」與「單一指標極致優化」之間存在內在權衡,尚未找到同時在所有軸線上都佔優的解法。消融實驗也顯示 IE 監督單獨使用會略微犧牲視覺通過率,AFE 單獨使用則不改善軌跡精度,說明三個軸線彼此之間存在一定程度的此消彼長,完整模型的「最佳平衡」更多是三者折衷的結果,而非各自同時達到最優。

### Related work

- 本論文與本頁「Robot-Specific Action-Conditioned World Models」主題下已收錄的 Ctrl-World、τ0-WM、WEAVER 等論文屬於同一技術脈絡,但切入角度不同——既有論文多半聚焦於「如何讓 world model 生成更好的 rollout 以輔助 policy 訓練」,本論文則反過來質疑「這些 world model 的 rollout 是否真的忠實跟隨指令動作」這一前提假設本身,屬於診斷/驗證層面的補充視角。其下游 policy 改進實驗採用 VLAW 式迭代框架,與本頁已收錄的 VLAW(Iterative Co-Improvement of VLA Policy and World Model)方法論高度相關,可視為對 VLAW 框架所依賴的「world model 模擬可信度」這一前提做系統性壓力測試。論文中做比較的 Cosmos-Predict2.5/Cosmos3 也已收錄於本頁「World Models as Data Engines」主題,顯示本論文的診斷結果對業界常用的 NVIDIA Cosmos 系列模型同樣適用。
- 判斷值得 survey 的程度:高。隨著越來越多 VLA 後訓練與 policy 評測流程開始依賴 world model 作為模擬器,本論文揭露的「專家-非專家支持落差」是一個此前被廣泛忽視、但對整個「world model 當模擬器」範式的可信度具有根本性影響的問題,其 WorldEcho benchmark 本身也可作為未來新 world model 論文的標準診斷工具,適合與本頁「World Model Evaluation & Physical-Reasoning Benchmarks」及「World Models as Data Engines / Simulators」主題交叉參照。

### Conclusion

- **綜合評價**:本論文填補了 AC-WM 評測方法論上一個長期被忽視的缺口——既有 benchmark 幾乎全部侷限於專家動作重播,而這與「world model 作為 policy 評測/改進模擬器」這一核心應用場景所需要的非專家動作跟隨能力存在系統性脫節。WorldEcho 的五類動作查詢設計與複合視覺-軌跡指標,為診斷這個問題提供了具體可操作的工具;WorldSync 則證明了透過分佈覆蓋擴增、表徵層級動態 grounding、介入效果監督三個互補軸線的組合,能在不犧牲太多單一指標的前提下取得更平衡的整體改善,且這種改善能實質轉化為下游 policy 在模擬與真實機器人上的改進效果(真實機器人任務 +20 個百分點 vs. 基線 +8 個百分點)。

- **與其他重要文章的關係**:本論文的診斷結果對本頁已收錄的多個 action-conditioned world model(Ctrl-World、τ0-WM、Cosmos 系列)具有直接的方法論警示意義,建議未來評測這類模型時應採用類似 WorldEcho 的非專家動作查詢協定,而非僅依賴專家重播。ROCm/AMD 在此領域尚待補強之處:WorldSync 的訓練涉及 flow-matching 影片擴散骨幹搭配 Action-Forcing Expert 輔助頭的聯合訓練,以及混合模擬/真實資料與多種非專家動作查詢類型的資料增強管線,這類複合損失函數(L_FM + AFE + IE)與多軸線資料混合的訓練配方目前預設執行於 NVIDIA GPU 生態(PyTorch + CUDA);隨着 AC-WM 作為機器人 policy 評測/改進模擬器的應用日益普及,且本論文證明了訓練資料分佈設計對下游效果有決定性影響,若 AMD 欲切入「world model 作為機器人模擬器」這一新興訓練基礎設施需求,及早驗證 ROCm 平台上 flow-matching 影片擴散模型搭配多輔助頭聯合訓練的穩定性與吞吐量,將是具體且有產業前瞻性的生態系拓展方向。
