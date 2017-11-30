---
title: "Last 函式 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 123b78a0-d6c9-4f78-b0e7-73b21854a250
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: f1a8a41eb518f251da3f99478d3733eaeae106e7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="report-builder-functions---last-function"></a>報表產生器函式 - Last 函式
  傳回所指定運算式給定範圍中的最後一個值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Last(expression, scope)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 (**變數** 或 **二進位**) 要執行彙總的運算式，例如 `=Fields!Fieldname.Value`。  
  
 *範圍 (scope)*  
 (**字串**) (選擇性) 包含要套用此函數之報表項目的資料集、資料區域或群組名稱。 如果未指定 *scope* ，則使用目前的範圍。  
  
## <a name="return-type"></a>傳回類型  
 由運算式的類型決定。  
  
## <a name="remarks"></a>備註  
 **Last** 函數會在指定的範圍已套用所有排序和篩選之後，以一組資料傳回最後的值。  
  
 **Last** 函數無法在群組篩選運算式中使用目前 (預設) 範圍以外的範圍。  
  
 您也可以在頁首中使用 **Last** ，從頁面的 **ReportItems** 集合傳回最後一個值，以產生會顯示頁面上第一個及最後一個項目的字典樣式標題。  
  
 *scope* 的值必須是字串常數，而且不得為運算式。 如果是未指定其他彙總的外部彙總， *scope* 必須參考目前的範圍或是包含的範圍。 如果是彙總的彙總，巢狀彙總可以指定子範圍。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的*Scope* 必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的*Scope* 不得為資料集的名稱。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函數。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例會傳回資料區的 `Category` 群組中的最後一個產品號碼。  
  
```  
=Last(Fields!ProductNumber.Value, "Category")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
