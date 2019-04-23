---
title: Aggregate 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 50a96884a5b97e0e4a287b0c731143dfa2d6e81f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969424"
---
# <a name="aggregate-function-report-builder-and-ssrs"></a>彙總函式 (報表產生器及 SSRS)
  傳回指定之運算式的自訂彙總，由資料提供者定義。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 要在其上執行彙總的運算式。 此運算式必須為簡單欄位參考。  
  
 *範圍 (scope)*  
 (`String`) 包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。 *Scope* 必須是字串常數，而且不得為運算式。 如果未指定 *scope* ，則使用目前的範圍。  
  
## <a name="return-type"></a>傳回類型  
 傳回類型是由資料提供者決定。 如果資料提供者不支援此函數或無法使用資料，則傳回 `Nothing`。  
  
## <a name="remarks"></a>備註  
 `Aggregate` 函數會提供一個方式來使用在外部資料來源上計算的彙總。 這個功能的支援是由資料延伸模組所決定。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料處理延伸模組會從 MDX 查詢擷取扁平化的資料列集。 結果集中的某些資料列可能會包含在資料來源伺服器上計算的彙總值。 這些值稱為 *「伺服器彙總」*(Server Aggregate)。 若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的圖形化查詢設計工具中檢視伺服器彙總，可以使用工具列的 **[顯示彙總]** 按鈕。 如需詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面 &#40;報表產生器&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)。  
  
 當您在 Tablix 資料區域的詳細資料列中顯示彙總和詳細資料集值的組合時，一般並不會包含伺服器彙總，因為這些值並非詳細資料。 不過，您可以顯示針對資料集所擷取的所有值，並自訂計算及顯示彙總資料的方式。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會在報表的運算式中偵測 `Aggregate` 函數的使用，以用來判斷是否要在詳細資料列中顯示伺服器彙總。 如果在資料區域的運算式中包含 `Aggregate`，則伺服器彙總只會顯示在群組總計或總計資料列中，而不會顯示在詳細資料列中。 如果想要在詳細資料列中顯示伺服器彙總，請不要使用 `Aggregate` 函數。  
  
 您可以藉由變更 **[資料集屬性]** 對話方塊的 **[將小計當做詳細資料列]** 選項值來變更這項預設行為。 當這個選項是設定為 `True` 時，所有的資料 (包括伺服器彙總) 會顯示為詳細資料。 當設定為 `False` 時，伺服器彙總會顯示為總計。 這個屬性的設定會影響連結至這個資料集的所有資料區域。  
  
> [!NOTE]  
>  所有參考 `Aggregate` 的報表項目的包含群組都必須有其群組運算式的簡單欄位參考，例如 `[FieldName]`。 您不能在使用複雜群組運算式的資料區域中使用 `Aggregate`。 若是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料處理延伸模組，則您的查詢必須包含 `LevelProperty` 類型 (而非`MemberProperty`) 的 MDX 欄位，才可支援使用 `Aggregate` 函數的彙總。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的*Scope* 必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的*Scope* 不得為資料集的名稱。  
  
-   *運算式*不得包含`First`， `Last`， `Previous`，或`RunningValue`函式。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>比較 Aggregate 和 Sum 函數  
 `Aggregate` 函數與 `Sum` 之類的數值彙總函式的不同點在於 `Aggregate` 函數會傳回資料提供者或資料處理延伸模組所計算的值。 之類的數值彙總函式`Sum`會傳回值，取決於資料集中的資料集由報表處理器計算*範圍*參數。 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) 中列出的彙總函式。  
  
## <a name="example"></a>範例  
 下列程式碼範例顯示的運算式會擷取欄位 `LineTotal`的伺服器彙總。 運算式會加到屬於群組 `GroupbyOrder`的資料列中的儲存格。  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
