---
title: "Level 函數 （報表產生器及 SSRS） |Microsoft 文件"
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
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 171842909a300d0c98fca2a26bbf4567810e8e95
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---level-function"></a>報表產生器函式-層級的函式
  傳回遞迴階層中之目前所在的層級。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (**字串**) (選擇性)。 包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。 如果未指定 *scope* ，則使用目前的範圍。  
  
## <a name="return-type"></a>傳回類型  
 傳回 **Integer**。 如果 *scope* 指定資料集或資料區，或指定非遞迴群組 (亦即，沒有 **Parent** 元素的群組)， **Level** 會傳回 0。 如果省略 *scope* ，則會傳回目前範圍的層級。  
  
## <a name="remarks"></a>備註  
 **Level** 函數傳回的值是以零為基礎；亦即，階層中的第一個層級是 0。  
  
 **Level** 函數可以在遞迴階層 (例如員工清單) 中提供縮排。  
  
 如需遞迴階層的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例提供 Employees 群組中的資料列層級：  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>請參閱＜  
 [報表 &#40; 中的運算式用法報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式 &#40; 中的資料類型報表產生器及 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、 彙總與內建集合 &#40; 的運算式範圍報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
