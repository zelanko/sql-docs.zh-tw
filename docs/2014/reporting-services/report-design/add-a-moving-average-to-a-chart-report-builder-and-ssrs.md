---
title: 將移動平均新增至圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 166cf9c1-0750-4866-8381-542e4fbfe65a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 016eeebb679ee16e07a99e44a3740efaae413483
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106833"
---
# <a name="add-a-moving-average-to-a-chart-report-builder-and-ssrs"></a>將移動平均加入至圖表 (報表產生器及 SSRS)
  移動平均是數列中資料的平均，是根據定義的一段時間而計算。 您可以在圖表上顯示移動平均以識別明顯的趨勢。  
  
 「移動平均」公式是技術分析中最常使用的價格指標。 您也可以從圖表上的數列衍生許多其他公式 (包括平均、中間值和標準差等)。 在指定移動平均時，每個公式都可能有一或多個必須指定的參數。  
  
 以設計模式加入移動平均公式時，所加入的線數列只是視覺化的預留位置。 圖表會在報表處理期間計算每個公式的資料點。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中不提供趨勢線的內建支援。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-calculated-moving-average-to-a-series-on-the-chart"></a>將導出的移動平均加入至圖表上的數列  
  
1.  以滑鼠右鍵按一下 **[值]** 區域中的欄位，然後按一下 **[加入導出數列]**。 **[導出數列屬性]** 對話方塊隨即開啟。  
  
2.  從 **[公式]** 下拉式清單中，選取 **[移動平均]** 選項。  
  
3.  為代表移動平均週期的 **[週期]** 指定整數值。  
  
    > [!NOTE]  
    >  週期是用來計算移動平均的天數。 如果沒有在 X 軸上指定日期/時間值，則週期會由用來計算移動平均的資料點數目代表。 如果只有一個資料點，則移動平均公式不會進行計算。 移動平均會從第二個點開始計算。 如果指定 **[從第一個點開始]** 選項，則移動平均會從圖表的第一個點開始。 如果只有一個資料點，則導出的移動平均中的點會與原始數列中的第一個點相同。  
  
## <a name="see-also"></a>另請參閱  
 [將圖表格式化 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [將空點加入至圖表 &#40;報表產生器和 SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
  
