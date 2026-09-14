---
layout: paper
title: "OpenVLA: An Open-Source Vision-Language-Action Model"
section: vla
page_id: "1945393020"
permalink: /vla/openvla-an-open-source-vision-language-action-model-1945393020/
---

**Paper** : [OpenVLA: An Open-Source Vision-Language-Action Model](https://arxiv.org/abs/2406.09246)  
**Source** : arXiv  
**arXiv ID** : 2406.09246

### Abstract

在 Internet 規模的視覺-語言資料與多樣機器人示範資料上預訓練的大型策略,有潛力改變機器人學習新技能的方式:不必從零訓練新行為,而是可以微調此類視覺-語言-動作(VLA)模型以獲得穩健、可泛化的視覺運動控制策略。然而,VLA 的廣泛採用面臨兩大挑戰:1) 現有 VLA 大多封閉、公眾難以取得;2) 先前工作未充分探索如何有效率地為新任務微調 VLA(這是採用的關鍵環節)。為此,作者提出 OpenVLA,一個 7B 參數的開源 VLA,訓練於 970k 筆真實世界機器人示範資料的多樣集合。OpenVLA 建立在 Llama 2 語言模型之上,結合融合了 DINOv2 與 SigLIP 預訓練特徵的視覺編碼器。得益於更多樣的資料與新模型組件,OpenVLA 在通用操作任務上表現優異,以 7 倍更少的參數量,在 29 個任務與多種機器人本體上,絕對任務成功率超越封閉模型 RT-2-X(55B)達 16.5%。作者進一步展示可有效微調 OpenVLA 以適應新場景,在涉及多物件的多任務環境中展現特別強的泛化結果與語言 grounding 能力,並以 20.4% 的優勢超越如 Diffusion Policy 等從零訓練的高表達力模仿學習方法。作者也探討計算效率,展示 OpenVLA 可透過現代低秩適應(LoRA)方法在消費級 GPU 上微調,並可透過量化高效服務而不損失下游成功率。最後,作者釋出模型檢查點、微調 notebook,以及內建支援在 Open X-Embodiment 資料集上大規模訓練 VLA 的 PyTorch 程式碼庫。

### Method

![Figure](/assets/images/1945393020_openvla_fig1.png) 

_Figure 1: OpenVLA overview_

![Figure](/assets/images/1945393020_openvla_fig2.png) 

_Figure 2: OpenVLA model architecture_

  * 要解決的問題:現有 VLA 大多封閉且缺乏公開的高效微調方法,阻礙了社群對 VLA 技術的採用與研究。
  * 主要方法:建立一個完全開源的 7B 參數 VLA 模型,結合開源語言模型骨幹(Llama 2)與融合視覺編碼器(DINOv2 + SigLIP),並在大規模、多樣化的真實機器人示範資料(970k 筆,源自 Open X-Embodiment)上訓練。
  * 與以往方式的差異:相較於 RT-2 等封閉模型,OpenVLA 完全開源(模型權重、微調程式碼、資料處理流程皆公開);相較於單一視覺編碼器,OpenVLA 融合 DINOv2(強調空間/幾何特徵)與 SigLIP(強調語意對齊特徵)兩種預訓練視覺特徵,提升視覺表徵品質;此外作者系統性探討了 LoRA 微調與量化部署方法,填補先前工作在「高效微調/部署」這塊的空白。
  * 重要方法設計描述:架構上,視覺輸入先分別通過 DINOv2 與 SigLIP 兩個視覺編碼器,將兩者的特徵融合後輸入 Llama 2 語言模型骨幹;動作輸出方式延續 RT-2 式的文字 token 離散化;訓練資料來自 Open X-Embodiment 收集的 970k 筆多機器人本體示範;微調階段可用 LoRA 等低秩適應方法在消費級 GPU(而非資料中心級硬體)上進行,部署階段可透過量化降低推論成本而不損失成功率。



### Result

  * 主要增強:在 29 個任務、多種機器人本體上,OpenVLA(7B)以遠少於 RT-2-X(55B)的參數量,絕對成功率超越後者 16.5%;在微調到新場景時,尤其在多物件多任務環境展現強泛化與語言 grounding 能力,並以 20.4% 優勢超越從零訓練的 Diffusion Policy;同時證明 LoRA 微調與量化部署不損失下游表現,兼顧了效能與計算效率。
  * 是否公正:OpenVLA 作為開源模型,其比較結果(尤其是超越 RT-2-X)已被後續多篇論文(如本次任務中的多篇 VLA 可解釋性論文)引用作為分析對象或基準,顯示其結果具有相當的社群認可度與可重現性,公正性較高。



### Limitation

  * 論文自陳/可推測的限制:(1) 動作仍以文字 token 離散化表示(延續 RT-2 的設計),在需要高頻、高精度連續控制的任務上可能有表達力限制,這也是後續 π0、GR00T 等模型改用 flow matching/diffusion 的原因之一;(2) 雖然支援 LoRA 微調與量化部署,但 7B 參數規模對於需要極低延遲的即時控制場景仍可能構成挑戰;(3) 970k 筆訓練資料雖然多樣,但仍以特定機器人本體集合(Open X-Embodiment 涵蓋的機型)為主,對於全新硬體本體的零樣本遷移能力需要查證全文。



### Related work

  * 本文中處理的多篇 VLA 可解釋性論文(如 Not All Features Are Created Equal, 2603.19233)將 OpenVLA 列為分析對象之一,顯示 OpenVLA 已成為 VLA 機制可解釋性研究的重要基準模型。
  * π0(2410.24164)、GR00T N1(2503.14734)等後續模型在動作輸出機制上(flow matching/diffusion vs 文字 token)代表了 OpenVLA 之後的技術演進方向。
  * 值得 survey 的程度極高:OpenVLA 是目前 VLA 領域最重要的開源基準模型之一,幾乎所有後續開源 VLA 研究都會參照或比較 OpenVLA。



### Conclusion

  * 綜合評價:OpenVLA 透過完全開源、高效微調與部署方案,大幅降低了 VLA 研究與應用的門檻,是 VLA 領域從「封閉大廠模型」走向「開放社群生態」的關鍵轉捩點,對整個領域的影響力極大,強烈建議參考。
  * 與其他重要文章的關係:OpenVLA 直接挑戰並在效能上超越 RT-2-X,同時是本次任務中多篇機制可解釋性論文(SAE、激活注入等分析)的重要研究對象,顯示其開源特性使其成為學術界研究 VLA 內部機制的首選平台之一。對 ROCm/AMD 而言,OpenVLA 完全開源、支援 LoRA 微調與量化部署,是目前最適合在 ROCm 生態系上驗證 VLA 訓練/推論支援度的候選模型之一——由於其權重與程式碼公開,理論上可直接測試在 AMD GPU 上的訓練與推論相容性與效能,這是本次任務清單中少數具備高度可操作性(可直接部署測試)的模型,值得 AMD 團隊優先評估作為 ROCm VLA 生態驗證的起點,但論文本身並未提及 ROCm 或 AMD 硬體的測試結果,此為基於其開源特性的合理延伸建議。