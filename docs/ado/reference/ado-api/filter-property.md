---
title: 篩選條件屬性 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72efa7b9a70bdfdf141c32d5487cc2a5b9776d16
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278757"
---
# <a name="filter-property"></a>篩選屬性
指出資料中的篩選[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回**Variant**值，其中可以包含下列項目之一：  
  
-   **準則字串：** 與串連的一個或多個個別的子句所組成的字串**AND**或**OR**運算子。  
  
-   **陣列的書籤：** 的唯一的書籤值陣列中的記錄該點**資料錄集**物件。  
  
-   A [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)值。  
  
## <a name="remarks"></a>備註

使用**篩選**以選擇性地篩選出記錄中的屬性**資料錄集**物件。 將已篩選**資料錄集**會變成目前的資料指標。 傳回值的其他屬性根據目前**游標**受到影響，例如[AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)， [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)， [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)，和[PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)。 設定**篩選**屬性設為特定的新值將目前的記錄移至第一筆記錄符合新值。
  
在表單中的子句組成準則字串*FieldName 運算子值*(例如， `"LastName = 'Smith'"`)。 您可以藉由串連個別的定序子句建立複合子句**AND** (例如， `"LastName = 'Smith' AND FirstName = 'John'"`) 或**OR** (例如， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 準則的字串，請使用下列指導方針：

-   *FieldName*必須是有效的欄位名稱從**資料錄集**。 如果欄位名稱包含空格，必須以方括號括住的名稱。  
  
-   運算子必須是下列其中之一： \<，>， \<=、 > =、 <>、 =、 或**像**。  
  
-   值是與您將會比較欄位值的值 (例如，'smith '距離，#8/24/95 # 12.345 或 $50.00)。 使用單引號字串和日期的井字號 （#）。 數字，您可以使用小數位數、 貨幣符號和科學記號標記法。 如果運算子**像**，值可以使用萬用字元。 允許只有星號 （*） 和百分比符號 （%） 萬用字元，以及它們必須是字串中的最後一個字元。 值不可以是 null。  
  
> [!NOTE]
>  若要篩選器值中包含單引號 （'），使用兩個單引號來代表其中一個。 例如，若要篩選 O'Malley，準則字串應該`"col1 = 'O''Malley'"`。 若要包含在開頭和結尾的篩選值的單一引號，括住的字串以井字符號 （#）。 例如，若要篩選 '1'，準則字串應該`"col1 = #'1'#"`。  
  
-   沒有任何優先順序之間 AND 或。 子句可加以群組括號內。 不過，無法群組子句或聯結，然後再加入群組到另一個子句 and，如下列程式碼片段所示：  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   相反地，您會建構為此篩選器  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   在**像**子句，您可以使用萬用字元在開頭和結尾的模式。 例如，您可以使用`LastName Like '*mit*'`。 或者**像**您可以只在模式結尾使用萬用字元。 例如， `LastName Like 'Smit*'`。  
  
 篩選條件常數更輕鬆地解決個別記錄的衝突，在批次更新模式，可讓您檢視，例如，只有那些記錄期間受到影響時最後一個[UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)方法呼叫。  
  
設定**篩選**屬性本身可能會因為基礎資料發生衝突。 例如，已由其他使用者刪除記錄時，可能會發生此失敗。 在這種情況下，提供者所傳回的警告，[錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不是停止執行程式。 只有當要求的所有記錄中都有衝突，就會發生在執行階段錯誤。 使用[Status 屬性 （ADO 資料錄集）](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性找出具有衝突的記錄。  
  
設定**篩選**屬性設為零長度字串 ("") 已使用相同的效果**adFilterNone**常數。
  
每當**篩選**設定屬性，則目前的記錄位置將移至第一個記錄中記錄的篩選子集**資料錄集**。 同樣地，當**篩選**清除屬性，移至第一筆記錄的目前記錄的位置**資料錄集**。

假設**資料錄集**進行篩選變數的型別，例如 sql_variant 類型的欄位上。 錯誤 (DISP_E_TYPEMISMATCH 或 80020005) 不相符的準則字串中使用的欄位和篩選值的子類型時，就會發生。 例如，假設：

- A**資料錄集**物件 (rs) 包含 sql_variant 類型的資料行 (C)。
- 並指派此資料行的欄位值為 1 的 I4 型別。 準則字串設定為`rs.Filter = "C='A'"`欄位上。

此設定會在執行階段產生錯誤。 不過，`rs.Filter = "C=2"`套用在同一個欄位將不會產生任何錯誤。 和欄位會從目前資料錄集篩選掉。

請參閱[書籤屬性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)如需說明，您可以從中建立要用於篩選屬性的陣列的書籤值的屬性。

篩選條件字串的格式會影響保存的內容僅**資料錄集**。 準則字串的範例是`OrderDate > '12/31/1999'`。 篩選器，建立書籤，或使用中的值的陣列**FilterGroupEnum**，不會影響保存的內容**資料錄集**。 這些規則套用至資料錄集與用戶端或伺服器端資料指標建立。
  
> [!NOTE]
>  當您套用 adFilterPendingRecords 旗標來篩選和修改**資料錄集**在批次更新模式中，產生**資料錄集**如果篩選為基礎的索引鍵的欄位是空的建立單一索引鍵的資料表和修改已根據索引鍵欄位的值。 產生**資料錄集**會為非空白如果為 true，下列陳述式的其中一個：  
  
-   以建立單一索引鍵資料表中的非索引鍵欄位為基礎的篩選。  
  
-   以建立多個索引鍵資料表中的任何欄位為基礎的篩選。  
  
-   建立單一索引鍵資料表中的非索引鍵欄位上進行修改。  
  
-   建立多個索引鍵資料表中的任何欄位上進行修改。  
  
下表摘要說明的效果**adFilterPendingRecords**以不同的篩選和修改的組合。 左欄則顯示可能的修改。 上的任何非索引鍵欄位，在建立單一索引鍵資料表中，索引鍵欄位上或任何為多個索引鍵資料表中的索引鍵欄位，就可以進行修改。 頂端列會顯示篩選準則。 篩選可以根據任何非索引鍵欄位中，建立單一索引鍵的資料表，或任何為多個索引鍵資料表中的索引鍵欄位中的索引鍵欄位。 交集的資料格會顯示結果。 A **+** 加號表示該套用**adFilterPendingRecords**導致非空白**資料錄集**。 A **-** 負號表示空**資料錄集**。  
  
||非索引鍵|單一索引鍵|多個索引鍵|
|-|--------------|----------------|-------------------|
|**非索引鍵**|+|+|+|
|**單一索引鍵**|+|-|不適用|
|**多個索引鍵**|+|不適用|+|
|||||
  
## <a name="applies-to"></a>適用於

[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[篩選器和 RecordCount 屬性範例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)
[篩選器和 RecordCount 屬性範例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)
[Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md) 
[最佳化屬性動態 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
