---
title: Previous 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 95a2dfb8ef3ac1420f243355f732daa246d81d0a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198538"
---
# <a name="previous-function-report-builder-and-ssrs"></a>Previous 函數 (報表產生器及 SSRS)
  傳回某個項目在指定之範圍內上一個執行個體的值或指定的彙總值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 (`Variant`或是`Binary`) 要用來識別資料的運算式和要擷取先前的值，例如`Fields!Fieldname.Value`或`Sum(Fields!Fieldname.Value)`。  
  
 *範圍 (scope)*  
 (`String`) 選擇性。 群組或資料區域中或 null 的名稱 (`Nothing`中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])，指定要從中擷取所指定的上一個值範圍*運算式*。  
  
## <a name="return-type"></a>傳回類型  
 傳回`Variant`或`Binary`。  
  
## <a name="remarks"></a>備註  
 `Previous` 函數會在套用過所有的排序和篩選之後，針對在指定範圍內評估的運算式傳回上一個值。  
  
 如果*運算式*未包含彙總，`Previous`函數會預設為報表項目目前的範圍。  
  
 在詳細資料群組中，使用`Previous`詳細資料列的上一個執行個體中指定之欄位參考的值。  
  
> [!NOTE]  
>  `Previous`函式只支援詳細資料群組中的欄位參考。 例如，在詳細資料群組的文字方塊中， `=Previous(Fields!Quantity.Value)` 會從上一個資料列傳回 `Quantity` 欄位的資料。 在第一個資料列中，這個運算式會傳回 Null (在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中為 `Nothing`)。  
  
 如果*運算式*包含使用預設範圍，彙總函式`Previous`彙總範圍的上一個執行個體內的資料呼叫所指定的彙總函式。  
  
 如果*運算式*包含彙總函式指定非預設值，範圍*範圍*參數`Previous`函式必須是包含範圍中指定的範圍彙總函式呼叫。  
  
 函式`Level`， `InScope`，`Aggregate`並`Previous`不適用於*運算式*參數。 不支援為任何彙總函式指定 *recursive* 參數。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列程式碼範例如果置於資料區域的預設資料列中，會為上一個資料列的 `LineTotal` 欄位提供值。  
  
### <a name="code"></a>程式碼  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>描述  
 下列程式碼範例顯示的運算式會計算月中特定日的銷售總和，以及該日在去年度的上一個值。 運算式會加到屬於子群組 `GroupbyDay`的資料列中的資料格。 該群組的父群組為 `GroupbyMonth`，這個群組的父群組又為 `GroupbyYear`。 運算式會顯示 GroupbyDay (預設範圍) 的結果，然後再顯示 `GroupbyYear` (GroupbyDay 父群組 `GroupbyMonth`的父代) 的結果。  
  
 例如，如果資料區域具有名為 `Year`的父群組，而其子群組名為 `Month`，該子群組的子群組又名為 `Day` (3 個巢狀層級)。 與群組 `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` 相關資料列中的運算式 `Day` 會針對去年度的同一日期和月份傳回銷售值。  
  
### <a name="code"></a>程式碼  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>另請參閱  
 [在報表中的運算式會使用&#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
