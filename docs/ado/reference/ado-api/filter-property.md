---
description: Filter 屬性
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a97db427db3c0dc42e004e1b0fcd0a889c9d6c5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443680"
---
# <a name="filter-property"></a>Filter 屬性
表示 [記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)資料的篩選。  
  
## <a name="settings-and-return-values"></a>設定和傳回值

設定或傳回 **Variant** 值，它可以包含下列其中一個專案：  
  
-   **準則字串：** 由一或多個與 **and** 或 **or** 運算子串連之個別子句所組成的字串。  
  
-   **書簽的陣列：** 唯一書簽值的陣列，這些值會指向記錄 **集** 物件中的記錄。  
  
-   [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)值。  
  
## <a name="remarks"></a>備註

使用 **Filter** 屬性可選擇性地顯示 **記錄集** 物件中的記錄。 篩選的 **記錄集會** 變成目前的資料指標。 根據目前資料 **指標** 傳回值的其他屬性會受到影響，例如 [ABSOLUTEPOSITION 屬性 (ado) ](../../../ado/reference/ado-api/absoluteposition-property-ado.md)、 [AbsolutePage 屬性 (ado) ](../../../ado/reference/ado-api/absolutepage-property-ado.md)、 [RecordCount 屬性 (ado) ](../../../ado/reference/ado-api/recordcount-property-ado.md)和 [PageCount 屬性 (ado) ](../../../ado/reference/ado-api/pagecount-property-ado.md)。 將 **篩選** 屬性設定為特定的新值，會將目前的記錄移至符合新值的第一筆記錄。
  
準則字串是由子句所組成，其格式為 *FieldName-運算子-Value* (例如 `"LastName = 'Smith'"`) 。 您可以藉由串連個別子句 **和和** (（例如 `"LastName = 'Smith' AND FirstName = 'John'"`) 或 **或** (例如) ）來建立複合子句 `"LastName = 'Smith' OR LastName = 'Jones'"` 。 針對準則字串，請使用下列指導方針：

-   *FieldName* 必須是 **記錄集中**有效的功能變數名稱。 如果功能變數名稱包含空格，您必須將名稱括在方括弧中。  
  
-   運算子必須是下列其中一項： \<, > 、 \<=, > =、 <>、= 或 **LIKE**。  
  
-   值是用來比較域值的值 (例如，' Smith '、#8/24/95 #、12.345 或 $50.00) 。 使用單引號搭配字串和井字元號 ( # ) 和日期。 若為數字，您可以使用小數點、貨幣符號和科學記號標記法。 如果運算子是 **LIKE**，則值可以使用萬用字元。 只允許星號 ( * ) 和百分比符號 (% ) 萬用字元，且必須是字串中的最後一個字元。 值不可以是 null。  
  
> [!NOTE]
>  若要在篩選值中加入單引號 ( ' ) ，請使用兩個單引號來表示一個。 例如，若要篩選 O'Malley，準則字串應該是 `"col1 = 'O''Malley'"` 。 若要在篩選值的開頭和結尾加上單引號，請使用井字型大小 ( # ) 來括住字串。 例如，若要篩選 ' 1 '，準則字串應該是 `"col1 = #'1'#"` 。  
  
-   AND 和 OR 之間沒有任何優先順序。 子句可以在括弧內分組。 不過，您不能將由或聯結的子句群組在一起，然後使用和將群組聯結至另一個子句，如下列程式碼片段所示：  
 `(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   相反地，您會將此篩選器視為  
 `(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   在 **LIKE** 子句中，您可以在模式的開頭和結尾使用萬用字元。 例如，您可以使用 `LastName Like '*mit*'`。 或者， **您可以在模式** 結尾使用萬用字元。 例如： `LastName Like 'Smit*'` 。  
  
 篩選準則常數可讓您在批次更新模式中，輕鬆地解決個別記錄衝突，例如，您可以只查看在最後一個 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md) 方法呼叫期間受影響的記錄。  
  
設定 **篩選** 屬性本身可能會因為與基礎資料發生衝突而失敗。 例如，當另一位使用者已刪除記錄時，可能會發生此錯誤。 在這種情況下，提供者會將警告傳回 [ (ADO) 集合的錯誤集合 ](../../../ado/reference/ado-api/errors-collection-ado.md) ，但不會停止程式執行。 只有當所有要求的記錄有衝突時，才會發生執行時間的錯誤。 您可以使用 [ [ (ADO 記錄集) ](../../../ado/reference/ado-api/status-property-ado-recordset.md) ] 屬性的 [狀態] 屬性來尋找有衝突的記錄。  
  
將 **Filter** 屬性設定為長度為零的字串 ( "" ) 與使用 **adFilterNone** 常數的效果相同。
  
每當設定 **篩選** 屬性時，目前的記錄位置會移至記錄 **集**內已篩選之記錄子集中的第一筆記錄。 同樣地，當清除 **篩選** 屬性時，目前的記錄位置會移至 **記錄集**內的第一筆記錄。

假設 **記錄集** 是根據某些變異類型的欄位進行篩選，例如類型 SQL_variant。 當準則字串中使用的欄位和篩選值的子類型不相符時，就會發生錯誤 (DISP_E_TYPEMISMATCH 或 80020005) 。 例如，假設：

-  (rs) 的 **記錄集** 物件包含 SQL_variant 類型 (C) 的資料行。
- 而且這個資料行的欄位已指派 I4 類型的值1。 準則字串會設定為 `rs.Filter = "C='A'"` 欄位上的。

此設定會在執行時間產生錯誤。 但是，套用 `rs.Filter = "C=2"` 在相同的欄位上不會產生任何錯誤。 而且會從目前的記錄集篩選出此欄位。

如需書簽值的說明，您可以在其中建立要與 Filter 屬性搭配使用的陣列，請參閱 [書簽屬性 (ADO) ](../../../ado/reference/ado-api/bookmark-property-ado.md) 屬性。

只有準則字串形式的篩選準則會影響保存的 **記錄集**的內容。 準則字串的範例為 `OrderDate > '12/31/1999'` 。 使用書簽陣列建立的篩選準則，或使用 **FilterGroupEnum**中的值，並不會影響保存的 **記錄集**的內容。 這些規則適用于使用用戶端或伺服器端資料指標所建立的記錄集。
  
> [!NOTE]
>  當您在批次更新模式中將 adFilterPendingRecords 旗標套用至已篩選和修改的 **記錄集** 時，如果篩選是以單一索引鍵的索引鍵欄位為基礎，而且是在索引鍵域值上進行修改，則結果 **集** 是空的。 如果下列其中一個陳述為真，則結果 **集** 將不會是空的：  
  
-   篩選是以單一索引資料表中的非索引鍵欄位為基礎。  
  
-   篩選是以多索引資料表中的任何欄位為基礎。  
  
-   在單一索引資料表的非索引鍵欄位上進行修改。  
  
-   在多索引資料表中的任何欄位上進行修改。  
  
下表摘要說明 **adFilterPendingRecords** 在不同的篩選和修改組合中的影響。 左邊的資料行顯示可能的修改。 您可以在任何非索引鍵欄位、單一索引鍵欄位中的索引鍵欄位，或在多索引鍵欄位中的任何索引鍵欄位上進行修改。 頂端資料列會顯示篩選準則。 篩選可以根據任何非索引鍵欄位、單一索引鍵欄位，或是多索引鍵資料表中的任何索引鍵欄位。 交集資料格會顯示結果。 **+** 加號表示將**adFilterPendingRecords**結果套用至非空白的**記錄集**。 **-** 負號表示空的**記錄集**。  
  
|組合|非索引鍵|單一金鑰|多個金鑰|
|-|--------------|----------------|-------------------|
|**非索引鍵**|+|+|+|
|**單一金鑰**|+|-|N/A|
|**多個金鑰**|+|N/A|+|
|||||
  
## <a name="applies-to"></a>套用至

[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[ (VB) ](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md) 
 的 Filter 和 RecordCount 屬性範例[ (VC + +) 的 Filter 和 RecordCount 屬性範例](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md) 
[ (ADO) ](../../../ado/reference/ado-api/clear-method-ado.md) 
 的 Clear 方法[優化屬性-動態 (ADO) ](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
