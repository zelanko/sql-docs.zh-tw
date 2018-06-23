---
title: Level 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 3df298cda1e6439d9c539c125689a3687cdc97f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136798"
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
 傳回`Integer`。 如果*範圍*指定為資料集或資料區，或指定非遞迴群組 (也就是不含群組`Parent`項目)，`Level`傳回 0。 如果省略 *scope* ，則會傳回目前範圍的層級。  
  
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
 [運算式會在報表中使用&#40;報表產生器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  