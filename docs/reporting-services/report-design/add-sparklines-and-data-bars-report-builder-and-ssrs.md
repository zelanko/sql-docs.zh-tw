---
title: "新增走勢圖和資料橫條 (報表產生器和 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 211700a96c3b38ed19977a02ba35743eb4eccc48
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>加入走勢圖和資料橫條 (報表產生器及 SSRS)
  走勢圖和資料橫條很小，也就是以少量的外來細節傳達許多資訊的精簡圖表。 如需詳細資訊，請參閱[走勢圖和資料橫條 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中，走勢圖和資料橫條最常放在資料表或矩陣內的資料格中。 走勢圖通常會針對每個資料格只顯示一個數列。 資料橫條可以包含一個或多個資料點。 走勢圖和資料橫條會從資料表或矩陣內每一個資料列的重複數列資訊來衍生其影響力。  
  
## <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>若要將走勢圖或資料橫條加入至資料表或矩陣  
  
1.  如果您還沒這樣做，請使用您想要顯示的資料建立 [資料表](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) 或 [矩陣](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md) 。  
  
2.  將資料行插入資料表或矩陣中。 如需詳細資訊，請參閱[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **[插入]** 索引標籤上，按一下 **[走勢圖]** 或 **[資料橫條]**，然後在新資料行的資料格內按一下。  
  
    > [!NOTE]  
    >  您無法將走勢圖放在資料表的詳細資料群組中。 它們必須放在與群組相關聯的資料格中。  
  
4.  在 [變更走勢圖類型/變更資料橫條類型] 對話方塊中，按一下您想要的走勢圖或資料橫條類型，然後按一下 [確定]。  
  
5.  按一下走勢圖或資料橫條。  
  
     隨即開啟 **[圖表資料]** 窗格。  
  
6.  在 [值] 區域中，按一下 [新增欄位] 的加號 (**+**)，然後按一下您想要將哪一個欄位的值加入圖表。  
  
7.  在 [類別目錄群組] 區域中，按一下 [新增欄位] 的加號 (**+**)，然後按一下您想要將哪一個欄位的值當作分組依據。  
  
     一般對於走勢圖或資料橫條而言，您不會將欄位加入至 **[數列群組]** 區域，因為您希望每一個資料列只有一個數列。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [在資料表或矩陣的圖表上對齊資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
