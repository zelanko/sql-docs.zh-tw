---
title: InScope 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ebf90710587c73206408dfda1429a90b58f39621
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228838"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>InScope 函數 (報表產生器及 SSRS)
  指出某個項目目前的執行個體是否在指定的範圍內。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (`String`) 的資料集、 資料區域中或指定範圍的群組名稱。  
  
## <a name="return-type"></a>傳回類型  
 傳回`Boolean`。  
  
## <a name="remarks"></a>備註  
 `InScope`函式會測試成員資格的目前執行個體的報表項目範圍中所指定之範圍*範圍*參數。  
  
 *Scope* 不能是運算式。  
  
 一般用法`InScope`函式在資料區域具有動態範圍。 比方說，`InScope`可以用在資料區域資料格中的鑽研連結，來提供不同的報表名稱和不同組的參數取決於按下哪一個儲存格。 此範例如下：  
  
-   下列運算式是用做鑽研連結中的報表名稱，如果按下的資料格是在 `ProductDetail` 群組中，便會開啟 `Month` 報表，如果不是，便開啟 `ProductSummary` 報表。  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   下列運算式會用於`Omit`屬性的鑽研報表參數，會將參數傳遞給目標報表才按下的儲存格是在`Product`群組。  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例指出項目目前的執行個體是否位在 `Product` 資料集、資料區域或群組的範圍中。  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>另請參閱  
 [在報表中的運算式會使用&#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
