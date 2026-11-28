---
layout: paper
title: "UniFuture: A 4D Driving World Model for Future Generation and Perception"
section: wm
page_id: "1996734598"
permalink: /zh/wm/unifuture-a-4d-driving-world-model-for-future-generation-and-perception-1996734598/
---

### Abstract

自駕車所處的物理世界本質上是四維的——由隨時間演化的 3D 空間幾何構成。因此,理想的駕駛世界模型(Driving World Model, DWM)應能模擬這種 4D 動態演化,使自車能預判周遭 3D 環境將如何變化。然而現有 DWM 要嘛專注於細緻的 2D 影片生成,卻忽略了底層的 3D 幾何結構(如深度),本質上只是在預測「電影般的幻覺」而非物理真實;要嘛是深度感知模型,擅長抽取高層幾何結構,卻僅限於當下或過去的靜態 3D 快照,缺乏預測這些結構將如何演化的能力。作者提出 UniFuture,一個統一的 4D 駕駛世界模型,同時預測未來場景外觀(RGB)與幾何(深度)。核心思路是將影像與對應深度圖視為同一 4D 現實的兩種投影,因此應在單一框架中聯合建模,而非分開處理。為此,論文引入 Dual-Latent Sharing(DLS)機制,將視覺與幾何兩種模態映射至共享的時空 latent 空間,隱式地將紋理與結構糾纏在一起;並提出 Multi-scale Latent Interaction(MLI)機制,強制雙向一致性——幾何約束視覺生成以防止結構性幻覺,視覺語意則精修幾何估計。在 nuScenes 與 Waymo 資料集上的大量實驗證明,此方法在未來生成與幾何感知兩方面均超越專門化模型,凸顯統一 4D 建模對自動駕駛的效益。本論文由 Dingkang Liang、Xiang Bai 等作者於 2025 年 3 月 17 日首次發佈於 arXiv,2026 年 2 月 26 日發佈 v2 修訂版,已確認獲 ICRA 2026 接受,屬於自駕世界模型領域「同時處理生成與感知」這一新興路線的代表性工作。

### Method

- **要解決的問題**:現有駕駛世界模型存在一個根本缺口——由大規模預訓練擴散模型驅動的近期 DWM 研究,多半只專注於細緻的 2D 像素層級影片生成,雖能合成視覺上逼真的 RGB 序列,卻忽略了底層 3D 幾何(如深度),本質上預測的是「電影般的幻覺」而非物理真實,導致模型在處理遮擋、估計精確距離等空間推理任務時表現不佳,生成結果可能視覺上合理卻物理上不一致。相對地,深度感知模型擅長抽取高層幾何結構,卻僅限於現在或過去的靜態 3D 快照,無法預測這些結構將如何隨時間演化,遺失了關鍵的時間維度。這兩類方法各自的侷限,指向一個尚待解決的問題:能否建立一個統一的駕駛世界模型,同時整合外觀、幾何與動態,預測駕駛場景真實的 4D 演化?

- **Main method**:UniFuture 建立在 SVD 影片生成框架(Vista)之上,透過兩個核心組件橋接外觀(RGB)與幾何(深度)這兩種異質但源自同一 4D 現實的投影。第一是 Dual-Latent Sharing(DLS)機制:不為深度估計訓練獨立的編碼器,而是讓影像序列與對應深度圖序列都通過同一個共享的預訓練 latent 編碼器,得到影像 latent 與深度 latent;影像 latent 走標準擴散流程建模時間動態,深度 latent 則透過 MLI 機制顯式推導,最終兩者都透過共享解碼器重建回像素/量測空間。這種設計迫使深度圖與自然影像共用同一 latent 空間,隱式運用影片生成器豐富的預訓練語意先驗來編碼幾何資訊,無需額外的深度專屬預訓練。第二是 Multi-scale Latent Interaction(MLI)機制,負責在外觀流與幾何流之間建立顯式雙向資訊流動:包含階層式深度層(從 UNet 編碼器與解碼器以 {1, 1/2, 1/4, 1/8} 多種尺度萃取特徵並逐層融合上採樣輸出,確保深度估計同時受益於高層語意脈絡與低層結構細節)、Inside Feedback(將中間深度 latent 特徵透過零初始化卷積注入回影片生成的 UNet 特徵流,使模型從標準影片生成起步,逐步學會運用幾何線索精修紋理合成)、以及 Outside Feedback(將最終預測的深度 latent 注入去噪後的影像 latent,確保最終外觀嚴格受預測幾何約束)。訓練目標結合影像與深度 latent 的重建損失,並額外加入遵循 Depth Anything 的 Scale- and Shift-Invariant 損失,確保預測幾何的物理有效性。推論時僅需單一當前影格,模型即可透過拼接 (M-1) 份高斯雜訊並經 MLI 強化的 UNet 演化,預測出完整的未來 4D 場景序列(影像-深度配對)。

- **和以往方式的差異**:與 GAIA-1、DriveDreamer、Vista、GenAD 等既有 DWM 相比,這些方法都僅專注於低層視覺表示的影片生成,忽略幾何資訊,因而缺乏空間推理能力;UniFuture 則是首個將未來場景生成與深度感知無縫整合、把世界建模從 2D 像素空間延伸至 4D 幾何空間的框架。與 Marigold、DepthCrafter 等深度估計方法相比,這些方法聚焦於感知當下或過去的環境,UniFuture 則將未來深度估計與世界模型整合,利用世界模型的推理能力來產生高品質深度預測,同時用精確的幾何線索強化動態場景建模——這種雙向互利的設計(而非將深度視為影片生成的附加任務)是論文宣稱的核心創新,DLS 與 MLI 兩個機制合力確保了這種雙向增益能真正落地,而非僅止於概念層次。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖對比既有方法與 UniFuture 的差異:(a) 純 2D 生成模型擅長合成逼真 RGB 序列卻忽略幾何,(b) 靜態 3D 感知模型擅長抽取幾何結構卻無法預測演化,(c) UniFuture 則同時預測未來外觀與幾何,真正建模 4D 世界演化;第二張圖展示完整訓練管線,呈現 Dual-Latent Sharing 如何將影像與深度統一映射至共享 latent 空間,以及 Multi-scale Latent Interaction 如何在外觀流與幾何流之間強制雙向時空一致性。

![Figure]({{ site.baseurl }}/assets/images/2503.13587_unifuture_teaser.png)

_Figure 1: 既有方法 vs. UniFuture——(a) 純 2D 影片生成忽略幾何,(b) 靜態 3D 感知缺乏時間演化,(c) UniFuture 聯合預測未來外觀與幾何,真正建模 4D 世界演化_

![Figure]({{ site.baseurl }}/assets/images/2503.13587_unifuture_architecture.png)

_Figure 2: UniFuture 訓練管線——Dual-Latent Sharing(DLS)將影像與深度映射至共享時空 latent 空間,Multi-scale Latent Interaction(MLI)強制外觀與幾何之間的雙向時空一致性_

### Result

- **主要增強部分**:在 nuScenes 資料集上,相較於強基線 Vista,UniFuture 在未來場景生成的 FID 指標上降低 3.7 分(從 15.5 降至 11.8,相對改善 23.9%),FVD 也達到有競爭力的水準(99.9 vs. 101.5);在深度估計方面,UniFuture 達到 AbsRel 8.936、δ1/δ2/δ3 分別為 91.4%/97.6%/98.9%,優於專門化的擴散式深度估計方法 Marigold(即便 Marigold 僅支援單幀深度估計,UniFuture 原生支援長達 25 幀的未來深度預測)。在 Waymo 資料集的零樣本泛化評測中,UniFuture 同樣全面超越 Vista(FID 16.3 vs. 23.8、FVD 227.6 vs. 238.4),且 Vista 完全不支援深度估計任務,顯示 UniFuture 的統一 4D 建模能力具備跨資料集的泛化性。消融實驗(Table III)進一步驗證了核心設計的必要性:比較「僅影像訓練」「僅深度訓練」「梯度分離訓練」「聯合訓練」四種優化範式,聯合訓練版本在生成(FID 11.8、FVD 99.9)與深度估計(AbsRel 8.936)兩方面均取得最佳平衡,顯著優於梯度分離版本(AbsRel 12.351),證明影像與深度的聯合最佳化(而非分開訓練後再組合)是效能提升的關鍵來源。

- **結果是否公正**:作者選擇與 Vista 這個公認強健的既有 DWM 基線做直接比較,並在相同解析度與迭代次數限制下,用 Vista 官方預訓練權重微調作為基線(標記為 ★),確保比較的公平性。深度估計方面也與 Marigold 這個深度估計領域的代表性擴散模型比較,而非僅挑選較弱的基線;作者也誠實標註 Marigold 原生僅支援單幀深度估計,為求合理比較特別訓練了以第 1 幀與第 12 幀為監督的版本,這種為基線方法做適配以確保公平比較的做法增加了結果的可信度。消融研究涵蓋優化範式、latent 表示、多尺度互動、雙向回饋機制、特徵對齊策略五個面向,顯示作者對核心設計選擇進行了全面的拆解驗證,而非僅展示最終模型的整體表現。

### Limitation

- **已知 limitation**:論文的方法描述與實驗部分並未明確討論模型的計算成本與推理延遲——DLS 與 MLI 機制涉及在影像與深度兩條 latent 流之間進行多尺度雙向特徵互動,其額外引入的計算開銷相對於純 2D 生成模型(如 Vista)的具體倍數,論文中未見詳細分析,這對於自動駕駛這類高度延遲敏感的應用場景而言,是值得後續關注但論文本身未充分展開的重要議題。

- **從 result 來看的弱項**:由於 nuScenes 與 Waymo 皆未提供密集的逐像素深度標註,論文採用 DepthAnythingV2 生成的偽深度標籤作為訓練與評測的真實值(ground truth),這意味著 UniFuture 的深度估計效能上限實質上受限於 DepthAnythingV2 本身的準確度,評測結果某種程度上是在衡量 UniFuture 與 DepthAnythingV2 偽標籤的一致性,而非絕對意義上的幾何真實性,這是論文方法論上一個值得注意但未被充分討論的侷限。此外,實驗僅使用前視單一相機作為主要訓練資料,尚未驗證多視角一致性生成能力,相較於 GAIA-2 等已支援多視角生成的同類工作,UniFuture 目前的驗證範圍仍相對侷限於單目場景。

### Related work

- UniFuture 與本頁「World Models for Autonomous Driving」主題下已收錄的多篇論文(DriVerse、WoTE、DreamerAD、EOT-WM、PhyGenesis、NVIDIA OmniDreams、Percept-WAM)同屬自駕場景世界模型研究,但切入角度形成有意義互補——既有收錄論文多聚焦於場景生成(DriVerse)、軌跡評測(WoTE)、強化學習(DreamerAD)、物理一致性修正(PhyGenesis)或感知增強(Percept-WAM),UniFuture 則是少數明確以「統一外觀與幾何的聯合 4D 建模」為核心訴求的工作,其 Dual-Latent Sharing 設計理念與本頁「Robot-Specific Action-Conditioned World Models」中強調統一表示的 GeniWorld(以 URDF 渲染視覺動作取代數值動作條件化)在設計哲學上有相通之處——兩者都試圖讓原本異質的模態(影像/深度,或影像/動作)共用同一表示空間,而非分別處理後再拼接。
- 判斷值得 survey 的程度:高。UniFuture 是少數同時在生成品質(FID/FVD)與幾何感知(AbsRel/δ 指標)兩條軸線上都提供完整定量驗證、且通過 ICRA 2026 同行評審的自駕世界模型論文,其「幾何與外觀應共享同一 latent 空間」的核心論點具有一定的方法論普適性,對於正在探索「視覺生成模型是否該為下游感知/規劃任務內建幾何先驗」這一自駕業界普遍關注問題的研究者具有高參考價值,適合與本頁「World Model Evaluation & Physical-Reasoning Benchmarks」主題交叉參照。

### Conclusion

- **綜合評價**:UniFuture 針對現有駕駛世界模型「要嘛只做 2D 生成、要嘛只做靜態 3D 感知」這一二元侷限,提出了一個簡潔但效果紮實的統一解法——透過共享 latent 空間與雙向特徵互動機制,讓外觀生成與幾何感知在同一框架內相互增強。論文在兩個資料集(含零樣本泛化到 Waymo)上的定量結果,以及涵蓋五個面向的詳盡消融實驗,為「聯合建模優於分開訓練」這個核心假設提供了有說服力的實證支持,且已通過 ICRA 2026 的同行評審,顯示其方法論獲得學界認可。

- **與其他重要文章的關係**:UniFuture 與本頁「World Models for Autonomous Driving」主題下的既有收錄論文形成互補視角,共同勾勒出自駕 world model 領域「視覺真實感」與「幾何一致性」兩條逐漸匯流的研究路線,也呼應本頁「Robot-Specific Action-Conditioned World Models」中關於統一多模態表示的設計思潮。ROCm/AMD 在此領域尚待補強之處:UniFuture 建立在 SVD 影片擴散框架之上,其 Dual-Latent Sharing 與 Multi-scale Latent Interaction 機制涉及多尺度 UNet 特徵萃取與雙向零卷積注入,訓練管線採用 DeepSpeed ZeRO-2 於 8 張 NVIDIA H20 GPU 上執行;隨著「生成式世界模型同時服務於自駕模擬、評測與訓練資料生成」逐漸成為中國與國際自駕供應商的共同技術路線(呼應本頁已收錄的 Wayve GAIA 系列、Percept-WAM 等工作),若 AMD 欲切入自駕世界模型的訓練與推理基礎設施市場,驗證此類雙流(影像+深度)latent 擴散架構在 ROCm 上搭配 ZeRO 分散式訓練策略的相容性與吞吐量表現,將是具體且有產業急迫性的生態系拓展方向。
