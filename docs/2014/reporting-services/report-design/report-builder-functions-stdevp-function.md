---
title: StDevP 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: cbcc0b3f-7b6d-4dd7-accb-cb375be8d852
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ec98ca344a86b2224f5e9a34c28ebe9ff8b488a6
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289176"
---
# <a name="stdevp-function-report-builder-and-ssrs"></a>StDevP 函數 (報表產生器及 SSRS)
  傳回運算式指定的所有非 Null 數值的母體標準差 (在給定範圍的內容中評估)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
StDevP(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 (`Integer` 或 `Float`) - 要在其上執行彙總的運算式。  
  
 *範圍 (scope)*  
 (`String`) 選擇性。 包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。 如果未指定 *scope* ，則使用目前的範圍。  
  
 *遞迴*  
 (**列舉型別**) 選擇性。 `Simple` (預設值) 或 `RdlRecursive`。 指定是否要以遞迴方式執行彙總。  
  
## <a name="return-type"></a>傳回類型  
 十進位運算式會傳回 `Decimal`，所有其他運算式都會傳回 `Double`。  
  
## <a name="remarks"></a>備註  
 運算式中指定的資料集必須具有相同的資料類型。 若要將具有多個數值資料類型的資料轉換成相同的資料類型，請使用 `CInt`、`CDbl` 或 `CDec` 等轉換函數。 如需詳細資訊，請參閱 [類型轉換函數](https://go.microsoft.com/fwlink/?LinkId=96142)。  
  
 *scope* 的值必須是字串常數，而且不得為運算式。 如果是未指定其他彙總的外部彙總， *scope* 必須參考目前的範圍或是包含的範圍。 如果是彙總的彙總，巢狀彙總可以指定子範圍。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的*Scope* 必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的*Scope* 不得為資料集的名稱。  
  
-   *運算式*不得包含`First`， `Last`， `Previous`，或`RunningValue`函式。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例提供 `Order` 群組或資料區域中之行項目總計的母體標準差。  
  
```  
=StDevP(Fields!LineTotal.Value, "Order")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
