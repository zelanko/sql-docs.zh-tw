---
title: Level 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a16e59709f3372a2460fa8847cdcc5c2c248bb2c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967464"
---
# <a name="level-function-report-builder-and-ssrs"></a>Level 函數 (報表產生器及 SSRS)
  傳回遞迴階層中之目前所在的層級。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>參數  
 *範圍 (scope)*  
 (`String`) (選擇性)。 包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。 如果未指定 *scope* ，則使用目前的範圍。  
  
## <a name="return-type"></a>傳回類型  
 傳回 `Integer`。 如果*領域*指定的資料集或資料區域，或指定非遞迴群組 (也就是沒有群組`Parent`項目)，`Level`會傳回 0。 如果省略 *scope* ，則會傳回目前範圍的層級。  
  
## <a name="remarks"></a>備註  
 `Level` 函數傳回的值是以零為基礎；亦即，階層中的第一個層級是 0。  
  
 `Level` 函數可以在遞迴階層 (例如員工清單) 中提供縮排。  
  
 如需遞迴階層的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例提供 Employees 群組中的資料列層級：  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
