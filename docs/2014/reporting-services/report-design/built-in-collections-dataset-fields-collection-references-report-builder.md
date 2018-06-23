---
title: 資料集 Fields 集合參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 635c108ec76177b90839ebb04d00d13dec7d1099
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133377"
---
# <a name="dataset-fields-collection-references-report-builder-and-ssrs"></a>資料集欄位集合參考 (報表產生器及 SSRS)
  報表中的每一個資料集都包含一個 Fields 集合。 Fields 集合是資料集查詢所指定的欄位加上您建立之任何其他導出欄位的集合。 當您建立資料集之後，欄位集合會出現在 **[報表資料]** 窗格中。  
  
 運算式中的簡單欄位參考會在設計介面上顯示為簡單運算式。 例如，當您將 `Sales` 欄位從 [報表資料] 窗格拖曳到設計介面上的資料表資料格時，就會顯示 `[Sales]` 。 這代表在文字方塊 Value 屬性上設定的基礎運算式 `=Fields!Sales.Value` 。 當報表執行時，報表處理器會評估此運算式，並將資料來源中的實際資料顯示在資料表資料格內的文字方塊中。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md) 和[資料集 Fields 集合 &#40;報表產生器及 SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>顯示資料集的欄位集合  
 若要顯示欄位集合的個別值，請將每一個欄位拖曳到資料表詳細資料列，並執行報表。 資料表之詳細資料列或清單資料區中的參考會顯示資料集中每一個資料列的值。  
  
 若要顯示欄位的摘要值，請將每一個數值欄位拖曳到矩陣的資料區。 總計資料列的預設彙總函式為 Sum，例如 `=Sum(Fields!Sales.Value)`。 您可以變更預設函數，以便能夠計算不同的總計。 如需詳細資訊，請參閱 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)。  
  
 若要將欄位集合的摘要值直接顯示在設計介面上的文字方塊中 (不屬於資料區的一部分)，您必須將資料集名稱指定為彙總函式的範圍。 例如，如果是名為 `SalesData`的資料集，下列運算式會針對 `Sales`: `=Sum(Fields!Sales,"SalesData")`欄位指定所有值的總計。  
  
 當您使用 [運算式] 對話方塊來定義簡單欄位參考時，可以在 [類別目錄] 窗格中選取 Fields 集合，並在 [欄位] 窗格中查看可用欄位的清單。 每個欄位都有數個屬性，包括 Value 和 IsMissing。 其餘的屬性會預先定義在擴充欄位屬性上，這些屬性可能可以提供給資料集使用 (視資料來源類型而定)。  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>偵測資料集欄位的 Null  
 若要偵測 Null 的欄位值 ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中為 `Nothing`)，您可以使用 `IsNothing` 函數。 當下列運算式放置於資料表詳細資料列的文字方塊內時，運算式會測試 `MiddleName` 欄位，並在該值為 Null 時以 "No Middle Name" 文字替代，而當該值不是 Null 時則為欄位值本身：  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>在執行階段偵測動態查詢的遺漏欄位  
 Fields 集合內的項目預設會有兩個屬性：Value 和 IsMissing。 IsMissing p 屬性會指出在設計階段針對資料集所定義的欄位是否包含在執行階段擷取的欄位中。 例如，您的查詢可能會呼叫預存程序 (其中的結果集會因為輸入參數而不同)，或者您的查詢可能會是 `SELECT * FROM` \<資料表> (變更資料表定義的地方)。  
  
> [!NOTE]  
>  IsMissing 會偵測設計階段與執行階段之間對於任何資料來源類型的資料集結構描述變更。 IsMissing 無法用來偵測多維度 cube 中的空白成員，並不相關的 MDX 查詢語言概念`EMPTY`和`NON EMPTY`。  
  
 您可以在自訂程式碼中測試 IsMissing 屬性，以判斷結果集中是否有欄位存在。 您不能搭配 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 函數呼叫 (如 `IIF` 或 `SWITCH`) 使用運算式來測試欄位是否存在，因為 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 會評估此函數呼叫中的所有參數，而當評估遺漏項目的參考時，這樣的處理會產生錯誤。  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>控制遺漏欄位之動態資料行可見性的範例  
 若要設定一個運算式來控制在資料集中顯示欄位之資料行的可見性，您必須定義一個自訂程式碼函數，根據欄位是否遺漏來傳回布林值。 例如，如果此欄位遺漏，下列自訂程式碼函數會傳回 True，如果此欄位存在則傳回 False。  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 若要使用此函數來控制資料行的可見性，請將此資料行的 Hidden 屬性設定為以下運算式：  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 當欄位不存在時，便會隱藏此資料行。  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>控制遺漏欄位之文字方塊值的範例  
 若要使用您撰寫的文字來取代遺漏欄位的值，您必須撰寫自訂程式碼，使其在欄位遺漏時可傳回用來取代欄位值的文字。 例如，下列自訂程式碼函數會在欄位存在時傳回欄位的值，而當欄位不存在時，則傳回您指定為第二個參數的訊息：  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 若要在文字方塊中使用這個函數，請將下列運算式加入到 Value 屬性：  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 此文字方塊會顯示欄位值或是您指定的文字。  
  
### <a name="using-extended-field-properties"></a>使用擴充欄位屬性  
 擴充欄位屬性是資料處理延伸模組在欄位上所定義的其他屬性，此模組是由資料集的資料來源類型所決定。 擴充欄位屬性是預先定義的，或是資料來源類型所特有的。 如需詳細資訊，請參閱 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)。  
  
 如果您指定不支援該欄位的屬性，則運算式評估為`null`(`Nothing`中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)])。 如果資料提供者不支援擴充的欄位屬性，或者找不到欄位的查詢執行時，屬性的值是否`null`(`Nothing`中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) 屬性的型別`String`和`Object`，和零 (0) 之屬性的型別`Integer`。 資料處理延伸模組可藉由最佳化包含這個語法的查詢來利用預先定義的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器和 SSRS&#41;](../report-data/report-datasets-ssrs.md)  
  
  