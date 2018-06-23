---
title: RunningValue 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 41f2345cf31347fba98448a02d4d3014b8883d73
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032947"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>RunningValue 函數 (報表產生器及 SSRS)
  傳回運算式指定的所有非 Null 數值的執行彙總 (在給定範圍中評估)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 要執行彙總的運算式，例如 `[Quantity]`。  
  
 *函數*  
 (`Enum`) 要套用至運算式，例如，彙總函式名稱`Sum`。 此函式不能`RunningValue`， `RowNumber`，或`Aggregate`。  
  
 *範圍 (scope)*  
 (`String`) 字串常數，它是資料集、資料區域或群組的名稱，或為 Null (在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中為 `Nothing`)，可指定要在其中評估彙總的內容。 `Nothing` 指定最外層的內容，通常為報表資料集。  
  
## <a name="return-type"></a>傳回類型  
 取決於 *function* 參數所指定的彙總函式。  
  
## <a name="remarks"></a>備註  
 值`RunningValue`重設為 0，每個範圍的新執行個體。 如果已指定群組，當群組運算式變更時，執行中的值也會重設。 如果已指定資料區域，就會為每個資料區域的新執行個體重設執行中的值。 如果已指定資料集，則整個資料集不會重設執行中的值。  
  
 `RunningValue` 不能用於篩選或排序運算式。  
  
 評估執行值的資料集合必須具有相同的資料類型。 若要轉換成相同的資料類型的多個數值資料類型的資料，使用轉換函式，例如`CInt`，`CDbl`或`CDec`。 如需詳細資訊，請參閱 [類型轉換函數](http://go.microsoft.com/fwlink/?LinkId=96142)。  
  
 *Scope* 不能是運算式。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的範圍必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的範圍不得為資料集的名稱。  
  
-   *運算式*不能包含`First`， `Last`， `Previous`，或`RunningValue`函式。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 若要計算資料列數的執行值，請使用 `RowNumber`。 如需詳細資訊，請參閱 [RowNumber 函式 &#40;報表產生器及 SSRS&#41;](report-builder-functions-rownumber-function.md)。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="examples"></a>範例  
 下列程式碼範例提供最外層範圍中 (也就是資料集) 名為 `Cost` 的欄位之執行總和。  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 下列程式碼範例提供名為 `Score` 的資料集中名為 `DataSet1`的欄位之累計總和。  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 下列程式碼範例提供最大範圍中名為 `Traffic Charges` 的欄位之累計總和。  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算式會在報表中使用&#40;報表產生器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  