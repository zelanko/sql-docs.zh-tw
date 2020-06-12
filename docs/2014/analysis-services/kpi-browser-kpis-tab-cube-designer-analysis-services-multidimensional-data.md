---
title: KPI 瀏覽器（Kpi 索引標籤，Cube 設計師）（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpibrowserpane.f1
ms.assetid: 2f61bde6-e6ec-4511-8645-c272374014ad
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1b6d15cbb75f3528546c566a72f8b23323df8772
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543710"
---
# <a name="kpi-browser-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>KPI 瀏覽器 (KPI 索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  在 Cube 設計師中，使用 [KPI]**** 索引標籤的 [KPI 瀏覽器]**** 窗格，即可檢視和測試關鍵效能指標 (KPI) 的結果。 流覽之前，kpi 必須先部署至 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 實例。  
  
> [!NOTE]  
>  此窗格只會顯示在瀏覽器檢視中。  
  
## <a name="options"></a>選項  
 **Subcube 方格**  
 這可用來定義 Subcube 和限制 [結果]**** 窗格中顯示的 KPI 結果。 方格包含下列資料行：  
  
 **大小**  
 選取要套用此篩選的維度。  
  
 **階層**  
 選取要套用此篩選的階層。  
  
 **運算子**  
 選取運算子，定義 [篩選運算式]**** 中的運算式如何套用至所選取階層。 下表描述可用的運算子。  
  
|值|描述|  
|-----------|-----------------|  
|**等於**|結果會限制為 **[篩選運算式]** 中定義的集合。|  
|**不等於**|結果會限制為 **[篩選運算式]** 中定義之集合所排除的成員。|  
|**位於**|結果會限制為 **[篩選運算式]** 中選擇的命名集。|  
|**不在**|結果會限制為 **[篩選運算式]** 中選擇之命名集所排除的成員。|  
|**包含**|結果會限制為成員名稱中包含 **[篩選運算式]** 中的字串之成員。|  
|**Begins With**|結果會限制為成員名稱是以 **[篩選運算式]** 中的字串開頭之成員。|  
|**Range (Inclusive)**|結果會限制為 **[篩選運算式]** 中選擇的範圍。|  
|**Range (Exclusive)**|結果會限制為 **[篩選運算式]** 中選擇之範圍所排除的成員。|  
|**MDX**|結果會限制為 [篩選運算式]**** 中的多維度運算式 (MDX) 運算式集合。|  
  
 **篩選運算式**  
 鍵入要由 [運算子]**** 評估的運算式，以限制要瀏覽的 KPI 結果。  
  
> [!NOTE]  
>  此欄位是一個動態資料輸入元素，外觀會變更以反映選取之運算子所需要的資料類型。  
  
 **結果方格**  
 依據 [篩選方格]**** 中定義的篩選，顯示 KPI 的評估值、目標、狀態及趨勢。 方格包含下列資料行：  
  
 **顯示結構**  
 顯示 Cube 包含的 KPI，並根據每一個 KPI 的 [顯示資料夾]**** 或 [父 KPI]**** 值來組織階層。  
  
 **ReplTest1**  
 顯示 KPI 的值。  
  
 **目的**  
 顯示 KPI 的目標值。  
  
 **狀態**  
 顯示 KPI 的狀態圖形。  
  
 **趨勢**  
 顯示 KPI 的趨勢圖形。  
  
 **Weight**  
 顯示 KPI 的加權因數。  
  
 **描述**  
 如果有提供 KPI 的描述，則顯示資訊圖示。  
  
 將游標停留在資訊圖示上，即可顯示 KPI 的工具提示 (包含描述)。  
  
> [!NOTE]  
>  如果在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上計算 KPI 時發生錯誤，此選項就會顯示錯誤的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [Kpi &#40;Cube 設計師&#41; &#40;Analysis Services-多維度資料&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
