---
title: 建立遞迴階層群組 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 92412bbde8a1032b34264ca254560f31704281e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135577"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>建立遞迴階層群組 （報表產生器及 SSRS）
  若要顯示遞迴資料，其中父系和子系之間的關聯性由資料集中的欄位，您可以將資料區群組運算式，根據子欄位，並將根據父欄位的父屬性。  
  
 遞迴階層群組，例如組織圖中的員工的常見用途是顯示階層式資料。 此資料集包含一份員工和經理，其中經理名稱也會出現在員工清單。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>建立遞迴階層  
 若要建立遞迴階層，在 tablix 資料區中，您必須設定的群組運算式的欄位，指定子資料並將指定的父資料的欄位群組的父屬性。 例如，包含員工識別碼和經理識別碼的欄位其中員工向經理，報告設定為員工識別碼和經理的父屬性的群組運算式的資料集的識別碼。  
  
 定義成遞迴階層 （也就是使用 Parent 屬性群組） 的群組可以有單一群組運算式。 您可以在文字方塊填補中，利用 `Level` 函式，根據員工在階層內的層級來縮排員工名稱。  
  
 如需詳細資訊，請參閱 <<c0> [ 加入或刪除資料區域中的群組&#40;報表產生器及 SSRS&#41; ](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)並[建立遞迴階層群組&#40;報表產生器及 SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)。</c0>  
  
### <a name="aggregate-functions-that-support-recursion"></a>支援遞迴的彙總函式  
 您可以使用接受參數的 Reporting Services 彙總函式*遞迴*針對遞迴階層計算摘要資料。 下列函數可接受`Recursive`做為參數：[總和](report-builder-functions-sum-function.md)， [Avg](report-builder-functions-avg-function.md)， [Count](report-builder-functions-count-function.md)， [CountDistinct](report-builder-functions-countdistinct-function.md)， [CountRows](report-builder-functions-countrows-function.md)， [Max](report-builder-functions-max-function.md)， [最小](report-builder-functions-min-function.md)， [StDev](report-builder-functions-stdev-function.md)， [StDevP](report-builder-functions-stdevp-function.md)， [Sum](report-builder-functions-sum-function.md)， [Var](report-builder-functions-var-function.md)，與[VarP](report-builder-functions-varp-function.md). 如需詳細資訊，請參閱 <<c0> [ 彙總函式參考&#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [資料表、 矩陣和清單&#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Tablix 資料區域&#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [彙總函式參考&#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [資料表&#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩陣&#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [列出&#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、 矩陣和清單&#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
