---
title: 新增空白點至圖表 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8a9cd8a292178d3800ecc9568fe5759b2a414f5a
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287626"
---
# <a name="add-empty-points-to-the-chart-report-builder-and-ssrs"></a>將空白點加入圖表中 (報表產生器及 SSRS)
  Null 值會顯示在圖表上，當做數列內資料點之間的空格或間距。 空點是指可以插入由 Null 值所建立之空格內的資料點。  
  
 根據預設，空點的計算方式是求得包含某個值之上一個和下一個資料點的平均值。 您可以變更這個值，好讓所有空白點都在零的地方插入。  
  
 如需詳細資訊，請參閱[圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-empty-points-on-a-chart"></a>在圖表上指定空白點  
  
1.  開啟 [屬性] 窗格。  
  
2.  在設計介面上，以滑鼠右鍵按一下包含 Null 值的數列。 數列的屬性會顯示在 [屬性] 窗格中。  
  
3.  展開 **[EmptyPoint]** 節點。  
  
4.  為 Color 屬性選取色彩值。  
  
5.  在 **[EmptyPoint]** 節點中，展開 [標記] 節點。  
  
6.  為 MarkerType 屬性選取標記類型。  
  
    > [!NOTE]  
    >  您必須選取一個標記類型，以便將空點加入至橫條圖、直條圖或散佈圖。 但如果是區域圖、折線圖和雷達圖，則選取標記類型為選擇性的動作，因為該圖表會填入空白的空格或間距，而不需要指定標記。  
  
7.  設定空點的值。  
  
    1.  在 [屬性] 窗格中，展開 **[CustomAttributes]** 節點。  
  
    2.  設定 EmptyPointValue 屬性。 若要在上一個和下一個資料點的平均值處插入空點，請選取 **Average**。 若要在零處插入空點，請選取 **Zero**。  
  
## <a name="see-also"></a>另請參閱  
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [圖表類型 &#40;報表產生器及 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [將刻度斷層加入至圖表 &#40;報表產生器及 SSRS&#41;](add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
