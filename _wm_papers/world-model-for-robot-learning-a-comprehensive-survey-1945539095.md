---
layout: paper
title: "World Model for Robot Learning: A Comprehensive Survey"
section: wm
page_id: "1945539095"
permalink: /wm/world-model-for-robot-learning-a-comprehensive-survey-1945539095/
---

**Paper** : [World Model for Robot Learning: A Comprehensive Survey](https://arxiv.org/abs/2605.00080)  
**Source** : arXiv（尚未標明特定會議發表）  
**arXiv ID** : 2605.00080

### Abstract

世界模型（world model）是對環境如何在動作條件下演變的預測性表徵，已成為機器人學習的核心組件,支援策略學習、規劃、模擬、評估與資料生成，並隨著基礎模型（foundation model）與大規模影片生成技術興起而快速發展。然而，現有文獻在架構、功能角色與具身應用領域上相當分散。本綜述從機器人學習的視角出發，系統性檢視世界模型如何與機器人策略耦合、如何作為強化學習與評估的學習型模擬器（learned simulator）、以及機器人視訊世界模型如何從「想像式生成」演進到「可控、結構化、基礎模型規模」的形式；並進一步將這些概念與導航（navigation）、自駕車連結，總結代表性資料集、基準測試與評估協議。作者承諾將持續維護配套的 GitHub repository。

### Method

![Figure](/assets/images/1945539095_survey_wm2_fig1.png) 

_Figure 1: Overview of the organization of this survey - architectural coupling of world models with robot policies, world models as simulators, and related evaluation/benchmarks._

  * **要解決的問題** ：world model 相關文獻分散於不同架構（latent dynamics、video diffusion 等）、不同功能角色（策略耦合、模擬器、資料生成器）與不同應用領域（操作、導航、自駕），缺乏系統性整理。
  * **Main method** ：這是一篇綜述（survey），並非提出新模型，而是建立一套分類框架，從三個角度組織文獻：(1) world model 與機器人策略如何耦合（例如作為策略的內部表徵或作為外部模擬器）；(2) world model 作為強化學習訓練與評估用的「學習型模擬器」的角色；(3) 機器人視訊世界模型從單純的「想像式生成」逐步演進至「可控、結構化、基礎模型規模」的技術脈絡。
  * **與以往方式的差異** ：相較於既有可能僅聚焦單一子領域（如僅操作或僅導航）的綜述，本文試圖橫跨機器人操作、導航與自駕車三大應用場景，提供一個更全面的統一視角，並特別強調 world model 與策略學習/強化學習/評估之間的功能性關係，而非只做架構分類。
  * **重要方法設計描述** ：文章架構預期依三條主軸展開：策略耦合面向（policy-coupled world model）、模擬器面向（learned simulator for RL/evaluation）、視訊生成面向（imagination-based to foundation-scale video world models），並在此基礎上補充資料集、基準測試（benchmark）與評估協議（evaluation protocol）的整理，最後連結到導航與自駕領域的對應應用。



### Result

  * 作為綜述論文，其「結果」體現在系統性地梳理與分類快速成長的 world model for robot learning 文獻，釐清關鍵範式（paradigm）與應用，並指出主要挑戰與未來方向。
  * 是否公正：由於是廣泛文獻回顧，其涵蓋範圍與分類是否全面、是否有遺漏重要工作，需要查證其他同期綜述（如清單中另兩篇 2606.00113、2511.02097）的分類方式是否一致或互補,以交叉驗證其完整性與客觀性。



### Limitation

  * 綜述類論文的限制在於：其分類框架反映作者主觀的組織方式，可能與其他綜述（例如同期的 2606.00113、2511.02097）採用不同的切分角度,導致讀者需要交叉比對才能得到較全面的認識。
  * 摘要未提供具體的量化評估或效能比較數據，其「結果」偏向質性整理而非量化證據，這是綜述類文章的通性限制。
  * 論文提及會持續維護 GitHub repository 以補充新工作,顯示作者也意識到此領域演進快速、當前版本可能很快過時。



### Related work

  * 本文與同一時期的另外兩篇 world model 綜述（arXiv:2606.00113《World Models for Robotic Manipulation: A Survey》、arXiv:2511.02097《A Step Toward World Models: A Survey on Robotic Manipulation》）在主題上高度重疊，值得交叉閱讀比較三者的分類框架異同。
  * 判斷 related work 值得 survey 的程度：高，本篇本身即為 survey，其列出的參考文獻與分類體系本身就是進一步追蹤 world model 領域具體技術論文（如 Aether、MimicGen、Dreamitate 等）的重要索引。



### Conclusion

  * 作為 2026 年較新的世界模型綜述,本文提供了一個橫跨策略、模擬器、視訊生成三個角度的統一框架,適合作為研究入門與快速掌握領域全貌的參考資料，值得優先閱讀。
  * 與其他重要文章的關係：本文可作為理解本次清單中其他具體技術論文（Aether、MimicGen、Dreamitate）在整體 world model 分類體系中定位的「地圖」，同時也應與同期的兩篇綜述互相比對，避免因單一綜述的分類偏好而產生片面理解。
  * ROCm/AMD 關聯性：作為文獻綜述，本文不涉及具體硬體實作細節，因此看不出與 ROCm/AMD 的直接關聯；但其中提及的「基礎模型規模的視訊世界模型」訓練與部署，隱含著對大規模 GPU 運算資源的高度需求，這類大規模訓練/推論在 ROCm 生態上的成熟度（相較於 CUDA 生態）是 AMD 在此領域布局時需要持續關注與補強的面向。