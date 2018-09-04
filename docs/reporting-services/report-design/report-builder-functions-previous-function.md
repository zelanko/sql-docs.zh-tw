---
title: Previous 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 01b2a6dc4b0d396fe6985ab0c4cefd689171fb2a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280854"
---
# <a name="report-builder-functions---previous-function"></a>報表產生器函式 - Previous 函式
  傳回某個項目在指定之範圍內上一個執行個體的值或指定的彙總值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 (**Variant** 或 **Binary**) 用來識別資料及擷取資料上一個值的運算式；例如， `Fields!Fieldname.Value` 或 `Sum(Fields!Fieldname.Value)`。  
  
 *範圍 (scope)*  
 (**字串**) 選擇性。 群組或資料區域的名稱，或為 Null (在**中為** Nothing [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])，指定範圍以從其擷取 *expression*所指定的上一個值。  
  
## <a name="return-type"></a>傳回類型  
 傳回 **Variant** 或 **Binary**。  
  
## <a name="remarks"></a>Remarks  
 **Previous** 函數會在套用過所有的排序和篩選之後，針對在指定範圍內評估的運算式傳回上一個值。  
  
 如果 *expression* 未包含彙總，則 **Previous** 函數會預設為報表項目的目前範圍。  
  
 在詳細資料群組中，請使用 **Previous** 來指定上一個詳細資料列執行個體中欄位參考的值。  
  
> [!NOTE]  
>  **Previous** 函數只支援詳細資料群組中的欄位參考。 例如，在詳細資料群組的文字方塊中， `=Previous(Fields!Quantity.Value)` 會從上一個資料列傳回 `Quantity` 欄位的資料。 在第一個資料列中，這個運算式會傳回 Null (在**中為** Nothing [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])。  
  
 如果 *expression* 包含使用預設範圍的彙總函式，則 **Previous** 會將彙總函式呼叫所指定範圍的上一個執行個體內的資料加以彙總。  
  
 如果 *expression* 包含的彙總函式指定預設外的範圍，則 *Previous* 函數的 **scope** 參數的範圍必須包含彙總函式呼叫所指定的範圍。  
  
 **Level**、 **InScope**、 **Aggregate** 和 **Previous** 函數不能用於 *expression*參數中。 不支援為任何彙總函式指定 *recursive* 參數。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>Description  
 下列程式碼範例如果置於資料區域的預設資料列中，會為上一個資料列的 `LineTotal` 欄位提供值。  
  
### <a name="code"></a>程式碼  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>Description  
 下列程式碼範例顯示的運算式會計算月中特定日的銷售總和，以及該日在去年度的上一個值。 運算式會加到屬於子群組 `GroupbyDay`的資料列中的資料格。 該群組的父群組為 `GroupbyMonth`，這個群組的父群組又為 `GroupbyYear`。 運算式會顯示 GroupbyDay (預設範圍) 的結果，然後再顯示 `GroupbyYear` (GroupbyDay 父群組 `GroupbyMonth`的父代) 的結果。  
  
 例如，如果資料區域具有名為 `Year`的父群組，而其子群組名為 `Month`，該子群組的子群組又名為 `Day` (3 個巢狀層級)。 與群組 `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` 相關資料列中的運算式 `Day` 會針對去年度的同一日期和月份傳回銷售值。  
  
### <a name="code"></a>程式碼  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
