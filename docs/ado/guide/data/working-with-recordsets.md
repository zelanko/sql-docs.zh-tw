---
title: 使用資料錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8e3c3c7ff7d623d3bec0adf60773266bb6e53571
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704438"
---
# <a name="working-with-recordsets"></a>使用資料錄集
**資料錄集**物件具有內建功能，可讓您重新排列結果集中資料的順序，來搜尋特定的記錄，根據您提供的準則，並且即使最佳化使用索引搜尋作業。 這些功能是否可供使用取決於提供者以及在某些情況下-例如屬於[Index](../../../ado/reference/ado-api/index-property.md)屬性-資料來源本身的結構。  
  
## <a name="arranging-data"></a>排列資料  
 通常，最有效率的方式來排序的資料中您**資料錄集**是用來傳回結果的 SQL 命令中指定 ORDER BY 子句。 不過，您可能必須變更中的資料順序**資料錄集**，已建立。 您可以使用**排序**屬性，以建立順序中的哪些資料列**資料錄集**會周遊。 此外，**篩選**屬性會決定哪些資料列會周遊資料列時，可以存取。  
  
 **排序**屬性會設定或傳回**字串**中的值，指出欄位名稱**資料錄集**用來排序。 每個名稱以逗號分隔，和 （選擇性） 後面接著一個空格，關鍵字**ASC** （排序的欄位以遞增順序） 或**DESC** （排序的欄位，以遞減順序）。 根據預設，如果未不指定任何關鍵字，則欄位會按照遞增順序。  
  
 因為資料不會實際重新排列，但可由索引指定的順序，排序作業會有效率。  
  
 **排序**屬性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設為**adUseClient**。 暫存索引將會建立每個欄位中指定**排序**如果索引不存在的屬性。  
  
 設定**排序**屬性設為空的字串將會重設為其原始順序的資料列，並刪除暫存的索引。 不會刪除現有的索引。  
  
 假設**Recordset**包含名為的三個欄位*firstName*， *middleInitial*，以及*lastName*。 設定**排序**屬性的字串"`lastName DESC, firstName ASC`"，將順序**資料錄集**依據姓氏的遞減順序，然後再依遞增順序的第一個名稱。 中間名首字母會被忽略。  
  
 沒有任何排序準則字串中所參考的欄位可以命名為"ASC"或"DESC"因為這些名稱衝突，以關鍵字**ASC**並**DESC**。 提供的欄位，使用具有衝突名稱別名**AS**中傳回的查詢關鍵字**資料錄集**。  
  
 如需詳細資訊**資料錄集**篩選，請參閱 < 在本主題稍後的 「 篩選結果 」。  
  
## <a name="finding-a-specific-record"></a>尋找特定的記錄  
 提供 ADO[尋找](../../../ado/reference/ado-api/find-method-ado.md)並[搜尋](../../../ado/reference/ado-api/seek-method.md)方法，找出特定資料錄中的**資料錄集**。 **尋找**方法支援的各種不同的提供者，但僅限於單一的搜尋準則。 **搜尋**方法支援搜尋多個條件，但不是支援的許多提供者。  
  
 欄位的索引可以大幅增強的效能**尋找**方法和**排序**並**篩選**屬性**資料錄集**物件。 您可以建立的內部索引**欄位**物件，藉由設定其動態[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)屬性。 此動態屬性加入至**屬性**的集合**欄位**物件，當您設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設**adUseClient**. 請記住這個索引是 ado 內部-您無法取得其存取權，或將它用於其他用途。 此外，這個索引會區別[Index](../../../ado/reference/ado-api/index-property.md)屬性**資料錄集**物件。  
  
 **尋找**方法快速找出資料行 （欄位） 的內部值**資料錄集**。 您時常可以增進的速度**尋找**方法所使用的資料行上**最佳化**在其上建立索引的屬性。  
  
 **尋找**方法會限制您的搜尋的一個欄位的內容。 **搜尋**方法需要的索引，並且具有其他限制也。 如果您必須搜尋未索引的基礎的多個欄位，或如果您的提供者不支援索引，您可以使用來限制結果**篩選條件**屬性**資料錄集**物件。  
  
### <a name="find"></a>尋找  
 **尋找**方法會搜尋**資料錄集**針對符合指定的準則的資料列。 （選擇性） 您可以指定搜尋開始的資料列及從起始的資料列位移的方向。 符合準則時，所找到的記錄; 上設定目前的資料列位置否則，位置會設定為結尾 （或起始） 的**資料錄集**，取決於搜尋方向。  
  
 只能在單一資料行名稱可以指定準則。 換句話說，這個方法不支援多重資料行的搜尋。  
  
 準則的比較運算子可以是" **>** 」 （大於）、 「 **\<** "（小於）、"="（等於）、"> ="（大於或等於）"< ="（小於或等於）、"<>"（不等於） 或"LIKE"（模式比對）。  
  
 臨界值可以是字串、 浮點數或日期。 字串值是以單引號或"#"（數字符號） 標記分隔 (比方說，」 狀態 = 'WA' 」 或 「 狀態 = #WA #")。 日期值會以"#"（數字符號） 標記 (例如，"start_date > #7/22/97 #")。  
  
 "Like"比較運算子時，星號 （*） 若要尋找的任何字元或子字串的一個或多個頁面時，可以包含的字串值。 例如，"等的狀態是\*' 」 符合 Maine 和麻省。 您也可以使用前置和尾端的星號來尋找位於值範圍內的子字串。 比方說，」 狀態，例如 '\*做為\*' 」 比對 Alaska、 阿肯色州和麻省。  
  
 星號可以使用只在準則字串結尾或一起開頭和結尾準則字串，如先前所示。 您不能使用星號做為前置字元的萬用字元 ('* str') 或內嵌萬用字元 ('s\*r')。 這會導致錯誤。  
  
### <a name="seek-and-index"></a>搜尋和編製索引  
 使用**Seek**方法並搭配**索引**屬性，如果基礎提供者支援上的索引**資料錄集**物件。 使用[支援](../../../ado/reference/ado-api/supports-method.md) **(adSeek)** 方法，以判斷基礎的提供者是否支援**搜尋**，而**Supports(adIndex)** 若要判斷提供者是否支援索引的方法。 (例如[OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支援**Seek**並**索引**。)  
  
 如果**Seek**尋找所需的資料列，沒有任何錯誤發生時，會和資料列位於結尾**資料錄集**。 設定**Index**所要的索引，然後再執行這個方法的屬性。  
  
 只有伺服器端資料指標才支援這個方法。 搜尋不支援在何時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性值**資料錄集**物件**adUseClient**。  
  
 可以使用這個方法時，才**資料錄集**物件使用開啟[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)的值**adCmdTableDirect**。  
  
## <a name="filtering-the-results"></a>篩選結果  
 **尋找**方法會限制您的搜尋的一個欄位的內容。 **搜尋**方法需要的索引，並且具有其他限制也。 如果您必須搜尋未索引的基礎的多個欄位，或如果您的提供者不支援索引，您可以使用來限制結果**篩選條件**屬性**資料錄集**物件。  
  
 使用**篩選條件**若要選擇性地篩選出記錄中的屬性**資料錄集**物件。 已篩選**資料錄集**會變成目前的資料指標，表示記錄不符合**篩選**條件不適用於**資料錄集**之前**篩選**已移除。 其他屬性會傳回目前的資料指標為基礎的值會受到影響，例如**AbsolutePosition**， **AbsolutePage**， **RecordCount**，和**PageCount**。 這是因為設定**篩選**設為特定值的屬性會將目前的記錄移至第一筆記錄符合新的值。  
  
 **篩選**屬性使用變數引數。 這個值表示使用三種方法之一**篩選條件**屬性： 準則字串**FilterGroupEnum**常數或書籤的陣列。 如需詳細資訊，請參閱本主題稍後的篩選條件字串，篩選與常數，與書籤的篩選。  
  
> [!NOTE]
>  當您知道您想要選取的資料時，會開啟通常更有效率**Recordset**使用 SQL 陳述式，它會有效地篩選結果集，而不是依賴**篩選**屬性。  
  
 若要移除的篩選器，從**Recordset**，使用**adFilterNone**常數。 設定**篩選條件**屬性設為零長度字串 ("") 已使用相同的效果**adFilterNone**常數。  
  
### <a name="filtering-with-a-criteria-string"></a>篩選條件字串  
 準則字串包含表單中的子句*FieldName 運算子值*(比方說， `"LastName = 'Smith'"`)。 您可以藉由串連的定序的個別子句所建立複合子句**AND** (例如`"LastName = 'Smith' AND FirstName = 'John'"`) 及**或者**(比方說， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 準則字串，請使用下列指導方針：  
  
-   *FieldName*必須是有效的欄位名稱，從**資料錄集**。 如果欄位名稱包含空格，必須以方括號括住的名稱。  
  
-   *運算子*必須是下列其中之一： **\<** ， **>** ， **\< =** ， **>=** **<>** ， **=** ，或**例如**。  
  
-   *值*是與您將會比較欄位值的值 (例如`'Smith'`， `#8/24/95#`， `12.345`，或`$50.00`)。 使用字串中使用單引號 （'） 與井字符號 (`#`) 的日期。 對於數字，您可以使用小數位數、 貨幣符號和科學記號標記法。 如果*運算子*是**像是**，*值*可以使用萬用字元。 只有星號 (\*) 和百分比符號 （%）允許萬用字元的字元，而且必須在字串中的最後一個字元。 *值*不可為 null。  
  
    > [!NOTE]
    >  若要在篩選中包含單引號 （'）*值*，使用兩個單引號來代表其中一個。 例如，若要篩選*O'Malley*，準則字串應該是`"col1 = 'O''Malley'"`。 若要包含在開頭和結尾的篩選值的單一引號，括住字串的井字號 （#）。 例如，若要篩選 *'1'* ，準則字串應該是`"col1 = #'1'#"`。  
  
 沒有任何優先順序之間**AND**並**或**。 子句可加以群組括號內。 不過，您無法群組子句聯結**或**然後將群組加入 AND，與另一個子句，如下所示。  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 相反地，您建構此篩選條件，如下所示。  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 中**等**子句中，您可以使用萬用字元的開頭和結尾模式 (例如`LastName Like '*mit*'`) 或只是在模式結尾 (比方說， `LastName Like 'Smit*'`)。  
  
### <a name="filtering-with-a-constant"></a>篩選與常數  
 下列常數可供篩選**資料錄集**。  
  
|常數|描述|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|檢視上次所影響的記錄篩選**刪除**，**重新同步處理**， **UpdateBatch**，或**CancelBatch**呼叫。|  
|**adFilterConflictingRecords**|檢視失敗的最後一個批次更新記錄的篩選條件。|  
|**adFilterFetchedRecords**|篩選器來檢視記錄中目前的快取-也就是從資料庫擷取記錄的最後一個呼叫的結果。|  
|**adFilterNone**|移除目前的篩選條件，並還原所有記錄進行檢視。|  
|**adFilterPendingRecords**|檢視只會記錄的篩選條件的已變更但尚未傳送至伺服器。 只適用於批次更新模式。|  
  
 篩選條件常數讓您更輕鬆地解決個別記錄的衝突，在批次更新模式，可讓您檢視，比方說，這些記錄，僅影響在最後一**UpdateBatch**方法呼叫中所示下列範例。  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>使用書籤篩選  
 最後，您可以在其中傳遞的 variant 的陣列的書**篩選**屬性。 產生的資料指標會包含其書籤傳遞給屬性的記錄。 下列程式碼範例會建立書籤的陣列中的記錄從**Recordset**具有"B" *ProductName*欄位。 接著，將陣列**篩選條件**關於產生已篩選的屬性，並顯示資訊**資料錄集**。  
  
```  
'BeginFilterBkmk  
Dim vBkmkArray() As Variant  
Dim i As Integer  
  
'Recordset created using "SELECT * FROM Products" as command.  
'So, we will check to see if ProductName has a capital B, and  
'if so, add to the array.  
i = 0  
Do While Not objRs.EOF  
    If InStr(1, objRs("ProductName"), "B") Then  
        ReDim Preserve vBkmkArray(i)  
        vBkmkArray(i) = objRs.Bookmark  
        i = i + 1  
        Debug.Print objRs("ProductName")  
    End If  
    objRs.MoveNext  
Loop  
  
'Filter using the array of bookmarks.  
objRs.Filter = vBkmkArray  
  
objRs.MoveFirst  
Do While Not objRs.EOF  
    Debug.Print objRs("ProductName")  
    objRs.MoveNext  
Loop  
'EndFilterBkmk  
```  
  
## <a name="creating-a-clone-of-a-recordset"></a>建立資料錄集的複製  
 使用**複製品**方法來建立多個重複**資料錄集**物件，特別是如果您想要維護一組指定的記錄中的多個目前資料錄。 使用**複製品**方法的效率高於建立並開啟新**資料錄集**具有相同的定義與原始物件。  
  
 目前的記錄，建立新建立的複製原先設定為第一筆記錄。 在複製目前的記錄指標**資料錄集**未同步處理與原始，反之亦然。 您可以在每個獨立巡覽**資料錄集**。  
  
 變更您對一**資料錄集**物件會顯示在所有其複製品，無論何種資料指標類型。 不過，您執行之後[Requery](../../../ado/reference/ado-api/requery-method.md)原始**資料錄集**，複製程式碼將不會再同步處理至原始。  
  
 關閉原始**資料錄集**不會關閉其複本，也不會關閉複本關閉原始或任何其他複本。  
  
 您可以複製**資料錄集**物件是否支援書籤。 書籤值是可互換的。也就是書籤參考從某個**資料錄集**物件是指任何其複製品中相同的記錄。
