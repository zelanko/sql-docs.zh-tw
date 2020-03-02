---
title: InScope 函式 (報表產生器) | Microsoft Docs
ms.date: 03/08/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 02ba83e15f22e28d3378996c98af4468ae425366
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081265"
---
# <a name="report-builder-functions---inscope-function"></a>報表產生器函式 - InScope 函式
  指出某個項目目前的執行個體是否在指定的範圍內。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (**字串**) 指定範圍之資料集、資料區或群組的名稱。  
  
## <a name="return-type"></a>傳回類型  
 傳回 **布林值**。  
  
## <a name="remarks"></a>備註  
 **InScope** 函數會測試報表項目目前執行個體的範圍，查看是否符合 *scope*參數所指定之範圍的成員資格。  
  
 *Scope* 不能是運算式。  
  
 **InScope** 函數一般會用於具有動態範圍的資料區。 例如，資料區資料格中的鑽研連結可以利用 **InScope** ，根據按下的資料格來提供不同的報表名稱和不同組的參數。 此範例如下：  
  
-   下列運算式是用做鑽研連結中的報表名稱，如果按下的資料格是在 `ProductDetail` 群組中，便會開啟 `Month` 報表，如果不是，便開啟 `ProductSummary` 報表。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   下列運算式會用於鑽研報表參數的 **Omit** 屬性，只有按下的資料格在 `Product` 群組中時，才會將參數傳給目標報表。  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例指出項目目前的執行個體是否位在 `Product` 資料集、資料區域或群組的範圍中。  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
