---
layout: paper
title: "NestedVLA: Learning to Consolidate and Generate Skills for Vision-Language-Action Models"
section: vla
page_id: "2610232710"
permalink: /zh/vla/nestedvla-learning-to-consolidate-and-generate-skills-for-vision-language-ac-2610232710/
---

### Abstract

視覺-語言-動作(VLA)模型可以學習涵蓋廣泛範疇的機器人技能,但將分別訓練的技能組合起來仍然十分困難——原始訓練資料可能因資料孤島(data silo)而無法用於聯合再訓練,而直接合併模型權重又會造成嚴重干擾。作者提出 NestedVLA,在無法取得原始訓練資料的前提下整合多個獨立微調的 VLA policy。NestedVLA 不將所有更新合併為單一 checkpoint,而是由嵌入 VLA 內部的超網路(hypernetwork)針對指定任務生成 action-expert 權重更新;每個任務各自壓縮儲存其視覺-語言模型(VLM)更新,兩者於推論時一併加到共享的凍結基座模型上。作者以開源 π0.5 骨幹在 MetaWorld、ManiSkill、CALVIN 三個強化學習微調 policy 上驗證 NestedVLA,平均成功率達 66.7%,較最強的模型合併基線高出 41.1 個百分點,在 ManiSkill 上與逐任務微調的差距僅 1 個百分點,在 CALVIN 上也大幅縮小落差;三個 policy 情境下總儲存量僅為單一完整 checkpoint 的 1.5 倍。本論文已被 NeurIPS 2026 接受(camera-ready 版本),作者來自香港理工大學計算學系。

### Method

- **要解決的問題**:機器人專用技能往往是在各自獨立的資料管線中訓練而成,原始訓練資料可能因資料孤島而無法用於聯合再訓練。常見的事後整合作法是將多個獨立微調的參數更新(task vector)合併為單一靜態 delta,但作者的權重空間分析發現,VLA 模型中不同任務學到的更新在主要參數群組上呈現微弱的對齊度(weak alignment),這種不相容性在直接主導控制輸出的 action expert 上尤其嚴重;簡單平均合併會讓多個獨立 policy 的效能幾乎全數喪失。這一觀察與既有的 MergeVLA 工作一致——後者同樣指出分散於 action-expert 各層的相依性是跨技能合併的主要障礙。

- **Main method**:NestedVLA 將整合問題的核心動詞從既有合併方法的「選擇(select)」——即任何輸出值都只是既有 task vector 集合的內插、遮罩或投影結果——轉變為「生成(generate)」。具體而言,policy 參數被拆為 VLM 部分 Θ^V 與 action-expert 部分 Θ^A;一個以任務身分 m 為條件的生成器 G_φ 直接產生 action-expert 的 delta τ̂_m^A = G_φ(m),而對應任務的壓縮 VLM delta z_m^V 則單獨保留,兩者於推論時都加到共享的凍結基座 Θ_0 上,組成任務專屬的 VLA policy。整套框架分三階段運作:(1) 技能習得(Skill Acquisition)——對每個任務 D_m 各自微調基座 Θ_0 得到 Θ_m,再透過「丟棄並重新縮放(drop-and-rescale)」壓縮法,將稠密的 task vector τ_m 轉換為稀疏技能表示 z_m = α·τ_m⊙M_m(α 為補償稀疏化能量損失的全域縮放因子,M_m 為逐模組 top-K 二元遮罩);作者比較了低位元量化、低秩分解、丟棄並重新縮放三種壓縮方式,發現 VLA fine-tuning 的 delta 呈現「稀疏量值主導」結構(少數元素集中了絕大部分的 ℓ2 能量),因此丟棄並重新縮放在保真度與壓縮率的權衡上明顯優於另外兩者,有別於 LLM SFT delta 通常更稠密、適合量化加低秩方案(如 D-QRELO)的情況。(2) 技能整合(Skill Consolidation)——將骨幹的每個權重張量切分為固定尺寸的二維 patch,每個 patch 由(參數類型、層索引、patch 座標)四項索引唯一定址,訓練單一「巢狀」超網路 G_φ 吸收全部 M 個任務的 action-expert 目標 {z_m^A};G_φ 內部包含逐任務 patch embedding、任務編碼器(2D 卷積加平均池化)、共享全連接主幹搭配逐任務 LoRA 路徑、以及逐任務多頭輸出模組五個可訓練元件,訓練目標為帶遮罩的多任務均方誤差。(3) 技能生成(Skill Generation)——推論時以目標任務 ID 查詢 G_φ 生成 action-expert delta,取回對應的壓縮 VLM delta,兩者一併與凍結基座組合實例化出該任務的 policy。

- **和以往方式的差異**:既有的靜態合併方法(平均法、TIES、WUDI、TSV-Merging 等)將所有 task vector 坍縮為單一共享 delta,在 VLA 設定下慘烈失敗——四種方法都讓 CALVIN 的 chain-completion 成功率降至 0%,顯示 VLA 表徵對參數擾動遠比既有方法原先驗證的 LLM SFT delta 更為敏感;既有的動態合併方法(TALL-Mask、EMR-Merging、Twin-Merging、Free-Merging)在推論時保留逐任務遮罩、純量或低秩殘差,雖然有所改善,但最強基線 Free-Merging 也僅達 25.6% 平均成功率,且需要 2.16 倍儲存開銷。無論靜態或動態,既有方法的共通操作動詞都是「選擇」——從已存在的 {θ_m - θ_0} 集合中內插、遮罩或投影;NestedVLA 則徹底改變這一前提,改由單一共享超網路針對任務身分直接「生成」action-expert delta,從根本上避免了跨任務參數衝突的問題,同時儲存成本僅 1.5 倍(低於除平均法以外所有合併基線),且不需要在推論時進行任何路由監督或改變前向架構。

- **關鍵方法圖**:見下方嵌入圖片——第一張圖對比既有模型合併方法與 NestedVLA 的核心概念差異:模型合併直接融合獨立微調的 VLA 權重,不相容的更新可能損害各自來源任務的表現;NestedVLA 則保留壓縮後的逐任務 VLM 更新,並以嵌入式任務條件超網路生成 action-expert 更新,兩者再與共享基座組合實例化出目標 policy。第二張圖展示 NestedVLA 完整三階段管線:技能習得(各任務獨立微調後壓縮為稀疏技能表示)、技能整合(單一巢狀超網路針對 action-expert 部分的壓縮目標訓練)、技能生成(推論時查詢超網路生成 delta,取回壓縮 VLM 更新,兩者與凍結基座組合)。

![Figure]({{ site.baseurl }}/assets/images/2610.23271_figure1.png)

_Figure 1: 模型合併 vs. NestedVLA 的核心概念對比——模型合併融合獨立微調權重可能造成干擾,NestedVLA 改以任務條件超網路生成 action-expert 更新並與壓縮 VLM 更新分別保留_

![Figure]({{ site.baseurl }}/assets/images/2610.23271_main_nested.png)

_Figure 2: NestedVLA 完整管線——技能習得、技能整合(單一巢狀超網路)、技能生成(推論時組合凍結基座)三階段流程_

### Result

- **主要增強部分**:在以開源 π0.5 作為共享骨幹、於 MetaWorld、ManiSkill、CALVIN 三個以強化學習微調的 policy 上進行的核心實驗中,逐任務獨立微調(無合併,作為效能上限參考)平均成功率為 80.5%。靜態合併方法全面失敗:簡單平均僅 14.8%,TIES、WUDI、TSV-Merging 等結合衝突消解、加權更新或奇異向量壓縮的方法反而都低於平均法,四者在 CALVIN 上全部降至 0% chain-completion。動態合併方法雖有改善但仍相對有限:TALL-Mask(2.09 倍儲存)22.6%、EMR-Merging(2.89 倍儲存)23.0%、Twin-Merging(2.25 倍儲存)25.3%、最強的 Free-Merging(2.16 倍儲存)25.6%。NestedVLA 以僅 1.5 倍儲存達到 66.7% 平均成功率,較最強動態合併基線 Free-Merging 高出 41.1 個百分點;在 ManiSkill 上達 87.2%,與逐任務微調上限(88.1%)僅相差 0.9 個百分點,在 CALVIN 上達到 75.0% 的 success_at_end,證明單一共享超網路足以在 chain-completion 級別的精細評測上保留技能品質。與逐任務上限的平均落差(-13.8 個百分點)幾乎全部集中在 MetaWorld 上。

- **結果是否公正**:論文系統性比較了靜態合併(Averaging、TIES、WUDI、TSV-Merging)與動態合併(TALL-Mask、EMR-Merging、Twin-Merging、Free-Merging)兩大類共七種代表性基線方法,並以逐任務獨立微調作為效能上限參照,同時報告每種方法的儲存成本以呈現效能-儲存權衡的全貌;論文附錄另外提供壓縮方式消融(量化 vs. 低秩 vs. 丟棄重縮放)、超網路三個任務條件元件(patch 路徑、LoRA 路徑、多頭路徑)的逐項消融、以及 MetaWorld 落後成因的專門分析(§4.4),顯示作者對結果穩健性有系統性的交代;然而,正如下方 Limitation 所述,驗證規模僅止於 3 個技能與模擬環境,尚未涵蓋更大規模技能集合或真實機器人場景。

### Limitation

- **已知 limitation**:作者在附錄 H 明確列出四項留待未來工作的限制:(i) 技能集合規模——所有實驗僅整合 M=3 個技能,尚未測量當 M 擴大一個數量級時,訓練時間、超網路容量或輸出品質如何變化;(ii) 新增技能的成本——目前新增一個技能需要擴充逐任務 patch embedding 表、逐任務多頭輸出,並重新訓練整個超網路,尚未展示如何以低成本增量方式加入未見過的技能;(iii) VLM 部分尚未整合——VLM 一半仍以逐任務 top-K 壓縮 delta 的形式各自保留,貢獻了 1.5 倍儲存預算中約 0.35 倍的部分,若能將超網路擴展至同時生成 VLM delta,可進一步壓低此下限,但留待未來工作(附錄 F 顯示單純的靜態 VLM 合併並不可行);(iv) 真實機器人驗證——所有數據均來自模擬 benchmark(MetaWorld、ManiSkill、CALVIN),尚未驗證遷移至實體硬體的表現。

- **從 result 來看的弱項**:與逐任務微調上限相比,NestedVLA 的平均落差幾乎全數集中在 MetaWorld 上(37.9% vs. 72.3% 上限),作者在 §4.4 將此歸因於 top-K 稀疏化預算本身的理想上限限制,顯示當技能本身的參數更新較難稀疏表示時,目前的壓縮方案會成為效能瓶頸,「自適應稀疏度」被作者明確點名為下一步最自然的改進方向。

### Related work

- NestedVLA 與本頁「Efficiency」主題下已收錄的多篇論文(如 VLA-Adapter、A Survey on Efficient Vision-Language-Action Models)同屬「讓 VLA 更易於規模化部署」的範疇,但切入角度互補:既有收錄論文多聚焦於單一 policy 內部的參數效率(蒸餾、小型化、量化),而 NestedVLA 關注的是「多個已訓練完成的 policy 之間」如何以極低儲存開銷共享一套骨幹,這是尚未被本頁收錄論文觸及的「後驗技能組合」問題。
- 本論文明確定位自己在模型合併文獻中的位置,指出既有靜態與動態合併方法的共通操作動詞皆為「選擇」,而 NestedVLA 轉向「生成」這一範式轉移與本頁「Architecture Paradigms」主題下聚焦動作解碼機制創新的論文(如 Discrete Diffusion VLA)形成有趣對比——後者改變的是單一 policy 內部「如何解碼動作」,NestedVLA 改變的則是「如何在多個 policy 之間共享與重組參數」,兩者分屬正交但同樣重要的 VLA 系統設計維度。
- 判斷值得 survey 的程度:高。NestedVLA 已確認為 NeurIPS 2026 接受的 camera-ready 論文,核心貢獻——將超網路應用於 VLA action-expert 的巢狀條件化生成,並系統性證明其優於七種具代表性的既有合併基線——具備清晰的方法論創新性;論文提供完整的消融實驗、權重空間診斷分析與公開程式碼,是近期少數明確處理「VLA 技能資料孤島」這一實務痛點的系統性工作。

### Conclusion

- **綜合評價**:NestedVLA 精準指出 VLA 領域中既有模型合併技術的核心盲點——這些技術多半是為 LLM SFT delta 的特性所設計,直接套用到對參數擾動更敏感的 VLA action expert 上會導致災難性的效能崩潰。作者提出的「參數生成取代參數選擇」範式轉移簡潔且實證有力,在三個強化學習微調 policy 上取得大幅優於既有合併基線的結果,同時維持相對低廉的儲存成本,為「資料孤島」這一機器人學界普遍存在的實務限制提供了具體可行的解方。

- **與其他重要文章的關係**:NestedVLA 可與本頁「Data, Benchmarks & Simulation」主題下強調跨具身、跨資料來源規模化訓練的論文(如 HuRo、EgoScale)形成互補視角——後者關注如何取得更多元的訓練資料來源,NestedVLA 則關注在資料無法集中取得的現實限制下,如何事後整合已分別訓練完成的技能,兩者共同指向「VLA 規模化」議題的一體兩面。ROCm/AMD 在此領域尚待補強之處:NestedVLA 的超網路架構涉及對十億級參數骨幹進行 patch 化的參數空間讀寫與逐任務稀疏遮罩運算,這類「以神經網路生成另一神經網路部分權重」的訓練模式,對底層深度學習框架在大規模參數張量的動態索引、稀疏遮罩運算效率與記憶體佈局管理上提出了獨特要求;隨著超網路式參數生成技術在多技能機器人部署場景中可能逐漸普及,及早驗證此類工作負載在 ROCm 軟體棧上的相容性與效能表現,將是值得關注的生態系拓展方向。
