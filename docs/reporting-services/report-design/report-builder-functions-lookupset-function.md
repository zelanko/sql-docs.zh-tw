---
title: LookupSet 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 7685acfd-1c8d-420c-993c-903236fbe1ff
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c4ceb9cd36d27a5c9fe29e0d446a56baf6698489
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689536"
---
# <a name="report-builder-functions---lookupset-function"></a>報表產生器函式 - LookupSet 函式
  從包含名稱/值組的資料集傳回符合指定之名稱的值組。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
LookupSet(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>參數  
 *source_expression*  
 (**Variant**) 在目前範圍中評估並指定要查閱之名稱或索引鍵的運算式。 例如， `=Fields!ID.Value`。  
  
 *destination_expression*  
 (**Variant**) 針對資料集中的每個資料列評估並指定要比對之名稱或索引鍵的運算式。 例如， `=Fields!CustomerID.Value`。  
  
 *result_expression*  
 (**Variant**) 對資料集的每個資料列進行評估，而且指定要擷取之值的運算式，其中 *source_expression* = *destination_expression*。 例如， `=Fields!PhoneNumber.Value`。  
  
 *資料集 (dataset)*  
 指定報表中資料集名稱的常數。 例如，"ContactInformation"。  
  
## <a name="return"></a>傳回  
 傳回 **VariantArray**或在沒有相符項目時傳回 **Nothing** 。  
  
## <a name="remarks"></a>Remarks  
 使用 **LookupSet** 可從具有一對多關係之名稱/值組的指定資料集中擷取一組值。 例如，如果是資料表中的客戶識別碼，您可以使用 **LookupSet** 從未繫結至資料區的資料集中，擷取該客戶的所有相關電話號碼。  
  
 **LookupSet** 會執行下列動作：  
  
-   評估目前範圍中的來源運算式。  
  
-   根據指定之資料集的定序，在已經套用篩選之後針對指定之資料集的每一個資料列評估目的地運算式。  
  
-   在每一個符合來源運算式和目的地運算式的項目上，針對資料集中的該資料列評估結果運算式。  
  
-   傳回結果運算式值的集合。  
  
 若要從具有一對一關聯性之名稱/值組的資料集中，擷取指定名稱的單一值，請使用 [Lookup 函式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md)。 若要針對一組值呼叫 **Lookup**，請使用 [Multilookup 函式 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md)。  
  
 系統會套用下列限制：  
  
-   當套用所有篩選運算式之後，便會評估**LookupSet** 。  
  
-   只支援一層的查閱。 來源、目的地或結果運算式不能包含查閱函數的參考。  
  
-   來源和目的地運算式必須評估為相同的資料類型。  
  
-   來源、目的地和結果運算式無法包含報表或群組變數的參考。  
  
-   **LookupSet** 不能當做下列報表項目的運算式使用：  
  
    -   資料來源的動態連接字串。  
  
    -   資料集中的導出欄位。  
  
    -   資料集中的查詢參數。  
  
    -   資料集中的篩選。  
  
    -   報表參數。  
  
    -   Report.Language 屬性。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，假設資料表繫結至一個資料集，此資料集包含銷售領域識別碼 TerritoryGroupID。 另一個資料集 "Stores" 包含領域中所有商店的清單，並包含領域識別碼 ID 和 StoreName 商店的名稱。  
  
 在下列運算式中， **LookupSet** 會比較 "Stores" 資料集中每一個資料列的 TerritoryGroupID 值與 ID。 在每次比對中，該資料列的 StoreName 欄位值都會加入至結果集。  
  
```  
=LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores")  
```  
  
## <a name="example"></a>範例  
 因為 **LookupSet** 會傳回物件的集合，所以您無法直接在文字方塊中顯示結果運算式。 您可以將集合中每一個物件的值串連起來當做一個字串。  
  
 使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函數 **Join** 從一組物件建立分隔的字串。 使用逗號當做分隔符號，在單一行中結合這些物件。 在某些轉譯器中，您可能會使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 換行字元 (`vbCrLF`) 當作分隔符號，在新行中列出每一個值。  
  
 當下列運算式作為文字方塊的 Value 屬性使用時，將會使用 **Join** 建立清單。  
  
```  
=Join(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"),",")  
```  
  
## <a name="example"></a>範例  
 如果是只轉譯幾次的文字方塊，您可能會選擇加入自訂程式碼產生 HTML，以便在文字方塊中顯示值。 文字方塊中的 HTML 需要額外的處理，所以如果是轉譯好幾千次的文字方塊，這並不是一個好的選擇。  
  
 將下列 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函數複製到報表定義中的程式碼區塊。 **MakeList** 會採用 *result_expression* 中所傳回的物件陣列，並使用 HTML 標記建立未排序的清單。 **Length** 會傳回此物件陣列中的項目數。  
  
```  
Function MakeList(ByVal items As Object()) As String  
   If items Is Nothing Then  
      Return Nothing  
   End If  
  
   Dim builder As System.Text.StringBuilder =   
      New System.Text.StringBuilder()  
   builder.Append("<ul>")  
  
   For Each item As Object In items  
      builder.Append("<li>")  
      builder.Append(item)  
   Next  
   builder.Append("</ul>")  
  
   Return builder.ToString()  
End Function  
  
Function Length(ByVal items as Object()) as Integer  
   If items is Nothing Then  
      Return 0  
   End If  
   Return items.Length  
End Function  
```  
  
## <a name="example"></a>範例  
 若要產生 HTML，您必須呼叫此函數。 將下列運算式貼到文字方塊的 Value 屬性中，並將文字的標記類型設定為 HTML。 如需詳細資訊，請參閱[將 HTML 新增至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md)。  
  
```  
=Code.MakeList(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"))  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
