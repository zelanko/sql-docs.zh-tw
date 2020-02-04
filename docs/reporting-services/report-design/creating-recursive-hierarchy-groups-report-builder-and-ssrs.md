---
title: 建立遞迴階層群組 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9125adcb007e7f191ab30bc0b957580d0012e859
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581512"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>建立遞迴階層群組 (報表產生器及 SSRS)
若要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 編頁報表中顯示遞迴資料，也就是父子關聯性是以資料集中的欄位來表示的情況，請根據子欄位來設定資料區群組運算式，並根據父欄位來設定 Parent 屬性。  
  
 顯示階層式資料是遞迴階層群組的常見用法，例如組織圖中的員工。 此資料集包含員工和經理的清單，經理名稱也會出現在員工清單內。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>建立遞迴階層  
 若要在 Tablix 資料區中建立遞迴階層，您必須將群組運算式設定為指定子資料的欄位，並將此群組的 Parent 屬性設定為指定父資料的欄位。 例如，如果是包含員工識別碼和經理識別碼之欄位的資料集 (員工向經理報告)，請將群組運算式設定為員工識別碼，並將 Parent 屬性設定為經理識別碼。  
  
 定義成遞迴階層的群組 (也就是使用 Parent 屬性的群組) 只能有單一群組運算式。 您可以在文字方塊填補中，利用 **Level** 函數，根據員工在階層內的層級來縮排員工名稱。  
  
 如需詳細資訊，請參閱[在資料區中新增或刪除群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 和[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)。  
  
### <a name="aggregate-functions-that-support-recursion"></a>支援遞迴的彙總函式  
 您可以使用接受 *Recursive* 參數的 Reporting Services 彙總函式，針對遞迴階層計算摘要資料。 下列函式接受 **Recursive** 當做參數： [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)、 [Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md)、 [Count](../../reporting-services/report-design/report-builder-functions-count-function.md)、 [CountDistinct](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md)、 [CountRows](../../reporting-services/report-design/report-builder-functions-countrows-function.md)、 [Max](../../reporting-services/report-design/report-builder-functions-max-function.md)、 [Min](../../reporting-services/report-design/report-builder-functions-min-function.md)、 [StDev](../../reporting-services/report-design/report-builder-functions-stdev-function.md)、 [StDevP](../../reporting-services/report-design/report-builder-functions-stdevp-function.md)、 [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)、 [Var](../../reporting-services/report-design/report-builder-functions-var-function.md)和 [VarP](../../reporting-services/report-design/report-builder-functions-varp-function.md)。 如需詳細資訊，請參閱 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)    
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
