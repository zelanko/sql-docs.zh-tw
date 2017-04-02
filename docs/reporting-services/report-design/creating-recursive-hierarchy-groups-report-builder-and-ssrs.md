---
title: "建立遞迴階層群組 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# 建立遞迴階層群組 (報表產生器及 SSRS)
若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 編頁報表中顯示遞迴資料，也就是父子關聯性是以資料集中的欄位來表示的情況，請根據子欄位來設定資料區群組運算式，並根據父欄位來設定 Parent 屬性。  
  
 顯示階層式資料是遞迴階層群組的常見用法，例如組織圖中的員工。 此資料集包含員工和經理的清單，經理名稱也會出現在員工清單內。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 建立遞迴階層  
 若要在 Tablix 資料區中建立遞迴階層，您必須將群組運算式設定為指定子資料的欄位，並將此群組的 Parent 屬性設定為指定父資料的欄位。 例如，如果是包含員工識別碼和經理識別碼之欄位的資料集 (員工向經理報告)，請將群組運算式設定為員工識別碼，並將 Parent 屬性設定為經理識別碼。  
  
 定義成遞迴階層的群組 (也就是使用 Parent 屬性的群組) 只能有單一群組運算式。 您可以在文字方塊填補中，利用 **Level** 函數，根據員工在階層內的層級來縮排員工名稱。  
  
 如需詳細資訊，請參閱[在資料區域中加入或刪除群組 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 和[建立遞迴階層群組 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)。  
  
### 支援遞迴的彙總函式  
 您可以使用接受 *Recursive* 參數的 Reporting Services 彙總函式，針對遞迴階層計算摘要資料。 下列函式接受 **Recursive** 當做參數： [Sum](../../reporting-services/report-design/sum-function-report-builder-and-ssrs.md)、 [Avg](../../reporting-services/report-design/avg-function-report-builder-and-ssrs.md)、 [Count](../../reporting-services/report-design/count-function-report-builder-and-ssrs.md)、 [CountDistinct](../../reporting-services/report-design/countdistinct-function-report-builder-and-ssrs.md)、 [CountRows](../../reporting-services/report-design/countrows-function-report-builder-and-ssrs.md)、 [Max](../../reporting-services/report-design/max-function-report-builder-and-ssrs.md)、 [Min](../../reporting-services/report-design/min-function-report-builder-and-ssrs.md)、 [StDev](../../reporting-services/report-design/stdev-function-report-builder-and-ssrs.md)、 [StDevP](../../reporting-services/report-design/stdevp-function-report-builder-and-ssrs.md)、 [Sum](../../reporting-services/report-design/sum-function-report-builder-and-ssrs.md)、 [Var](../../reporting-services/report-design/var-function-report-builder-and-ssrs.md)和 [VarP](../../reporting-services/report-design/varp-function-report-builder-and-ssrs.md)。 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md)。  
  
## 請參閱＜  
 [資料表、矩陣和清單 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)    
 [資料表、矩陣和清單 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  