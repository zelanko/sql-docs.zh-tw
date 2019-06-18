---
title: RunningValue 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 91447a23f04b05dc27d0ddcc47ba845d3dc313a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65577177"
---
# <a name="report-builder-functions---runningvalue-function"></a>報表產生器函式 - RunningValue 函式
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
 (**Enum**) 運算式所要套用的彙總函式名稱，例如 **Sum**。 此函數可以是 **RunningValue**、 **RowNumber**或 **Aggregate**。  
  
 *範圍 (scope)*  
 (**String**) 字串常數，它是資料集、資料區或群組的名稱，或為 Null (在**中為** Nothing [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])，可指定要在其中評估彙總的內容。 **Nothing** 指定最外層的內容，這通常為報表資料集。  
  
## <a name="return-type"></a>傳回類型  
 取決於 *function* 參數所指定的彙總函式。  
  
## <a name="remarks"></a>Remarks  
 **RunningValue** 的值會針對範圍的每個新執行個體重設為 0。 如果已指定群組，當群組運算式變更時，執行中的值也會重設。 如果已指定資料區域，就會為每個資料區域的新執行個體重設執行中的值。 如果已指定資料集，則整個資料集不會重設執行中的值。  
  
 **RunningValue** 不能用於篩選或排序運算式。  
  
 評估執行值的資料集合必須具有相同的資料類型。 若要將具有多個數值資料類型的資料轉換成相同的資料類型，請使用 **CInt**、 **CDbl** 或 **CDec**等轉換函數。 如需詳細資訊，請參閱 [類型轉換函數](https://go.microsoft.com/fwlink/?LinkId=96142)。  
  
 *Scope* 不能是運算式。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的範圍必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的範圍不得為資料集的名稱。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函數。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 若要計算資料列數的執行值，請使用 **RowNumber**。 如需詳細資訊，請參閱 [RowNumber 函式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-rownumber-function.md)。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
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
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
