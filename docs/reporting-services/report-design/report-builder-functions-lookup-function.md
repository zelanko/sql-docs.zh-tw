---
title: "Lookup 函數 （報表產生器及 SSRS） |Microsoft 文件"
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
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4426bffe23295c623d0bba5592c1488cb0ede770
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---lookup-function"></a>報表產生器函式-查閱函式
  從包含名稱/值組的資料集傳回第一個符合指定之名稱的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>參數  
 *source_expression*  
 (**Variant**) 在目前範圍中評估並指定要查閱之名稱或索引鍵的運算式。 例如， `=Fields!ProdID.Value`。  
  
 *destination_expression*  
 (**Variant**) 針對資料集中的每個資料列評估並指定要比對之名稱或索引鍵的運算式。 例如， `=Fields!ProductID.Value`。  
  
 *result_expression*  
 (**Variant**) 對資料集的每個資料列進行評估，而且指定要擷取之值的運算式，其中 *source_expression* = *destination_expression*。 例如， `=Fields!ProductName.Value`。  
  
 *資料集 (dataset)*  
 指定報表中資料集名稱的常數。 例如，"Products"。  
  
## <a name="return"></a>傳回  
 傳回 **Variant**，或在沒有相符項目時傳回 **Nothing** 。  
  
## <a name="remarks"></a>備註  
 使用 **Lookup** 可從具有一對一關係之名稱/值組的指定資料集中擷取值。 例如，如果是資料表中的識別碼欄位，您可以使用 **Lookup** 從未繫結至資料區的資料集中，擷取對應的名稱欄位。  
  
 **Lookup** 會執行下列動作：  
  
-   評估目前範圍中的來源運算式。  
  
-   根據指定之資料集的定序，在已經套用篩選之後針對指定之資料集的每一個資料列評估目的地運算式。  
  
-   在第一個符合來源運算式和目的地運算式的項目上，針對資料集中的該資料列評估結果運算式。  
  
-   傳回結果運算式值。  
  
 若要針對具有一對多關係的單一名稱或索引鍵欄位擷取多個值，請使用 [LookupSet 函數 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md)。 若要呼叫**查閱**針對一組值中，使用[Multilookup 函數 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md).  
  
 系統會套用下列限制：  
  
-   當套用所有篩選運算式之後，便會評估**Lookup** 。  
  
-   只支援一層的查閱。 來源、目的地或結果運算式不能包含查閱函數的參考。  
  
-   來源和目的地運算式必須評估為相同的資料類型。 傳回類型與評估之結果運算式的資料類型相同。  
  
-   來源、目的地和結果運算式無法包含報表或群組變數的參考。  
  
-   **Lookup** 不能當做下列報表項目的運算式使用：  
  
    -   資料來源的動態連接字串。  
  
    -   資料集中的導出欄位。  
  
    -   資料集中的查詢參數。  
  
    -   資料集中的篩選。  
  
    -   報表參數。  
  
    -   Report.Language 屬性。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，假設資料表繫結至一個資料集，此資料集包含產品識別碼 ProductID 的欄位。 另一個資料集 "Product" 包含對應的產品識別碼 ID 和產品名稱 Name。  
  
 在下列運算式中， **Lookup** 會比較 "Product" 資料集之每一個資料列中 ProductID 與 ID 的值，而且當找到符合的項目時，就會傳回該資料列的 Name 欄位值。  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>請參閱＜  
 [報表 &#40; 中的運算式用法報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式 &#40; 中的資料類型報表產生器及 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、 彙總與內建集合 &#40; 的運算式範圍報表產生器及 SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
