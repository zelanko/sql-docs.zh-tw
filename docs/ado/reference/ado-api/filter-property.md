---
title: 篩選屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cede9be7c484d40c2220fc891779f7dfb6e5a8df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028145"
---
# <a name="filter-property"></a>Filter 屬性
表示資料的篩選條件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回**Variant**值，其中可包含下列項目之一：  
  
-   **準則字串：** 字串串連在一起的一或多個個別的子句組成**AND**或是**OR**運算子。  
  
-   **書籤的陣列︰** 值的唯一的書籤的陣列中的記錄當時**資料錄集**物件。  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)值。  
  
## <a name="remarks"></a>備註

使用**篩選條件**若要選擇性地篩選出記錄中的屬性**資料錄集**物件。 已篩選**資料錄集**變成目前的游標。 傳回值的其他屬性會根據目前**游標**會受到影響，例如[AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)， [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)，並[PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)。 設定**篩選**屬性設為特定的新值會將目前的記錄移至第一筆記錄符合新的值。
  
準則字串在表單中的子句組成*FieldName 運算子值*(比方說， `"LastName = 'Smith'"`)。 您可以藉由串連的定序的個別子句所建立複合子句**AND** (例如`"LastName = 'Smith' AND FirstName = 'John'"`) 或**OR** (比方說， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 準則的字串，請使用下列指導方針：

-   *FieldName*必須是有效的欄位名稱，從**資料錄集**。 如果欄位名稱包含空格，必須以方括號括住的名稱。  
  
-   運算子必須是下列其中之一： \<，>， \<=、 > =、 <>、 =、 或**像**。  
  
-   值是與您將會比較欄位值的值 (例如，'Smith'，#8/24/95 # 12.345 或 $50.00)。 使用單引號字串與日期的井字號 （#）。 對於數字，您可以使用小數位數、 貨幣符號和科學記號標記法。 運算子是否**像**，值可以使用萬用字元。 只有星號 （*） 和百分比符號 （%）可以使用萬用字元，而且必須在字串中的最後一個字元。 值不可以是 null。  
  
> [!NOTE]
>  若要在篩選值中包含單引號 （'），使用兩個單引號來代表其中一個。 例如，若要篩選 O'Malley，準則字串應該是`"col1 = 'O''Malley'"`。 若要包含在開頭和結尾的篩選值的單一引號，括住字串加上井字符號 （#）。 例如，若要篩選 '1'，準則字串應該是`"col1 = #'1'#"`。  
  
-   沒有任何優先順序之間 AND 和或。 子句可加以群組括號內。 不過，您無法群組子句或聯結，並將加入 and，如下列程式碼片段所示的另一個子句中的群組：  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   相反地，您會建構為此篩選器  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   在 **像**子句中，您可以使用萬用字元的開頭和結尾的模式。 例如，您可以使用`LastName Like '*mit*'`。 或使用**像**您只能在模式結尾使用萬用字元。 例如， `LastName Like 'Smit*'` 。  
  
 篩選條件常數讓您更輕鬆地解決個別記錄的衝突，在批次更新模式，可讓您檢視，比方說，這些記錄，僅影響在最後一[UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)方法呼叫。  
  
設定**篩選**屬性本身可能會因為與基礎資料發生衝突。 例如，另一位使用者已刪除記錄時，會發生此失敗。 在此情況下，提供者會傳回警告[錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不會不會中斷程式執行。 只有當所有要求的記錄上會發生衝突，就會發生在執行階段錯誤。 使用[Status 屬性 (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性找出具有衝突的記錄。  
  
設定**篩選條件**屬性設為零長度字串 ("") 已使用相同的效果**adFilterNone**常數。
  
每當**篩選條件**屬性設定，目前的記錄位置將移至第一個記錄中記錄的篩選子集**資料錄集**。 同樣地，當**篩選條件**清除屬性，則目前的記錄位置移動中的第一個記錄**資料錄集**。

假設**資料錄集**篩選根據某些變數的類型，例如 sql_variant 類型的欄位。 錯誤 (DISP_E_TYPEMISMATCH 或 80020005) 不相符的準則字串中使用的欄位和篩選值的子類型時，就會發生。 例如，假設：

- A**資料錄集**物件 (rs) 包含 sql_variant 類型的資料行 (C)。
- 並指派此資料行的欄位值為 1 的 I4 型別。 準則字串會設定為`rs.Filter = "C='A'"`欄位上。

此設定會在執行階段產生錯誤。 不過，`rs.Filter = "C=2"`套用在同一個欄位將不會產生任何錯誤。 和欄位會篩選出目前的記錄集。

請參閱[書籤屬性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)以了解您可以用來建置的 Filter 屬性搭配使用陣列的書籤值的屬性。

僅篩選條件字串的格式會影響保存的內容**資料錄集**。 準則字串的範例是`OrderDate > '12/31/1999'`。 使用書籤，或使用中的值的陣列建立的篩選條件**FilterGroupEnum**，並不會影響保存的內容**資料錄集**。 這些規則適用於建立與用戶端或伺服器端資料指標的資料錄集。
  
> [!NOTE]
>  當您將 adFilterPendingRecords 旗標套用至篩選時，修改**資料錄集**批次的更新模式，結果**資料錄集**如果已根據篩選的索引鍵欄位是空的為單一索引鍵的資料表所作的修改是對索引鍵欄位值。 結果**資料錄集**將為非空白如果下列陳述式的其中一種情況：  
  
-   以單一索引的資料表中的非索引鍵欄位為基礎的篩選。  
  
-   篩選根據多個索引資料表中的任何欄位。  
  
-   已修改為單一索引鍵資料表中的非索引鍵欄位上。  
  
-   已修改為多個索引鍵的資料表中的任何欄位。  
  
下表摘要說明的效果**adFilterPendingRecords**以不同的篩選及修改的組合。 左欄則顯示可能的修改。 上的任何非為索引鍵欄位，在單一索引的資料表中，索引鍵的欄位或任何為多個索引鍵資料表中的索引鍵欄位，就可以進行修改。 頂端列會顯示篩選的準則。 篩選可以根據任何非為索引鍵欄位，在單一索引的資料表，或任何為多個索引鍵資料表中的索引鍵欄位的索引鍵欄位。 交集的資料格會顯示結果。 A **+** 正號表示該套用**adFilterPendingRecords**導致非空白**資料錄集**。 A **-** 負號表示空白**資料錄集**。  
  
||非索引鍵|單一索引鍵|多個索引鍵|
|-|--------------|----------------|-------------------|
|**非索引鍵**|+|+|+|
|**單一索引鍵**|+|-|N/A|
|**多個索引鍵**|+|N/A|+|
|||||
  
## <a name="applies-to"></a>適用於

[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[Filter 和 RecordCount 屬性範例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[Filter 和 RecordCount 屬性範例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
[Optimize 動態屬性 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
