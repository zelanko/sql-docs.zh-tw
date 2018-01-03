---
title: "使用資料錄集 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Recordset object [ADO]
ms.assetid: bdf9a56a-de4a-44de-9111-2f11ab7b16ea
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a861030b8ec30e176d7535d6e2f7976a87c0832a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="working-with-recordsets"></a>使用資料錄集
**資料錄集**物件具有內建功能，可讓您重新整理結果集中資料的順序，來搜尋特定的記錄，根據您提供的準則，並且甚至最佳化使用索引搜尋作業。 這些功能是否可供使用取決於提供者，以及在某些情況下，例如的[索引](../../../ado/reference/ado-api/index-property.md)屬性 — 資料來源本身的結構。  
  
## <a name="arranging-data"></a>排列資料  
 通常，最有效率的方式來排序的資料中您**資料錄集**是用來傳回結果的 SQL 命令中指定 ORDER BY 子句。 不過，您可能必須變更中的資料順序**資料錄集**，已建立。 您可以使用**排序**屬性，以建立順序中的哪些資料列**資料錄集**會周遊。 此外，**篩選**屬性會決定哪些資料列會周遊資料列時，可以存取。  
  
 **排序**屬性設定或傳回**字串**名稱中的值，指出欄位**資料錄集**用來排序。 每個名稱以逗號隔開，而且是可選擇性地接著一個空格和關鍵字**ASC** （排序的欄位，以遞增順序） 或**DESC** （排序的欄位，以遞減順序）。 根據預設，如果未不指定任何關鍵字，則欄位會依遞增順序。  
  
 因為資料不會實際重新排列，但存取索引所指定的順序，排序作業會有效率。  
  
 **排序**屬性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 將會建立暫存索引，每個欄位中指定**排序**屬性，如果索引不存在。  
  
 設定**排序**屬性設為空字串將會重設為其原始順序的資料列，並刪除暫存索引。 將不會刪除現有的索引。  
  
 假設**資料錄集**包含名為三個欄位*firstName*， *middleInitial*，和*lastName*。 設定**排序**屬性至字串"`lastName DESC, firstName ASC`」，將順序**資料錄集**依據姓氏的遞減順序，然後依名字的遞增順序。 中間名首字母會被忽略。  
  
 沒有排序準則字串中所參考的欄位可以命名為"ASC"或"DESC"因為這些名稱衝突和關鍵字**ASC**和**DESC**。 提供具有衝突名稱別名使用的欄位**AS**關鍵字，查詢中傳回**資料錄集**。  
  
 如需有關**資料錄集**篩選，請參閱 < 在本主題稍後的 「 篩選結果 」。  
  
## <a name="finding-a-specific-record"></a>尋找特定的記錄  
 ADO 提供[尋找](../../../ado/reference/ado-api/find-method-ado.md)和[搜尋](../../../ado/reference/ado-api/seek-method.md)方法，找出特定資料錄中的**資料錄集**。 **尋找**方法支援的各種不同的提供者，但僅限於單一搜尋準則。 **搜尋**方法支援搜尋多個條件，但不是支援的許多提供者。  
  
 在欄位上的索引可以大幅改善的效能**尋找**方法和**排序**和**篩選**屬性**資料錄集**物件。 您可以建立的內部索引**欄位**物件藉由設定其動態[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)屬性。 此動態屬性加入至**屬性**集合**欄位**物件時設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**. 請記住此索引是 ADO 內部 — 您無法取得其存取權，或將它用於其他用途。 此外，此索引是與不同[索引](../../../ado/reference/ado-api/index-property.md)屬性**資料錄集**物件。  
  
 **尋找**方法快速找出資料行 （欄位） 的內部值**資料錄集**。 您時常可以增進速度**尋找**方法所使用的資料行上**最佳化**其上建立索引的屬性。  
  
 **尋找**方法限制搜尋範圍，以一個欄位的內容。 **搜尋**方法需要您具有索引，並具有其他限制也。 如果您必須搜尋不是索引，基礎的多個欄位，或如果您的提供者不支援索引，您可以使用來限制結果**篩選**屬性**資料錄集**物件。  
  
### <a name="find"></a>尋找  
 **尋找**方法會搜尋**資料錄集**滿足指定的條件的資料列。 （選擇性） 您可以指定搜尋開始的資料列及從起始的資料列位移的方向。 如果符合條件時，所找到的記錄; 上設定目前資料列位置否則，會結束 （或開始） 的設定位置**資料錄集**，端視搜尋方向。  
  
 只能在單一資料行名稱可以指定準則。 換句話說，這個方法不支援多重資料行的搜尋。  
  
 準則的比較運算子可以是"**>**」 （大於）、"**\<**"（小於）、"="（等於）、"> ="（大於或等於），"< ="（小於或等於）、"<>"（不等於） 或 [讚] （模式比對）。  
  
 臨界值可以是字串、 浮點數或日期。 字串值會以單引號或"#"（數字符號） 標記分隔 (例如，"狀態 = 'WA'"或"狀態 = #WA #")。 日期值會以"#"（數字符號） 標記分隔 (例如，"start_date > #7/22/&#97;")。  
  
 如果比較運算子 [讚]，字串值可以包含星號 （*） 來尋找一個或多個出現的任何字元或子字串。 例如，"類似的狀態是\*'"符合 Maine 和 Massachusetts。 您也可以使用前置和尾端的星號，若要尋找的子字串，包含值範圍內。 比方說，「 狀態類似 '\*為\*'"比對阿拉斯加、 阿肯色州和 Massachusetts。  
  
 星號可以使用只在準則字串結尾或一起開頭和結尾準則字串，如先前所示。 您無法使用星號做為前置萬用字元 ('* str') 或內嵌萬用字元 ('s\*r')。 這會導致錯誤。  
  
### <a name="seek-and-index"></a>搜尋和編製索引  
 使用**搜尋**方法並搭配**索引**如果基礎提供者在支援索引屬性**資料錄集**物件。 使用[支援](../../../ado/reference/ado-api/supports-method.md)**(adSeek)**方法，以判斷基礎提供者是否支援**搜尋**，而**Supports(adIndex)**若要判斷提供者是否支援索引的方法。 (例如， [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支援**搜尋**和**索引**。)  
  
 如果**搜尋**找不到所需的資料列，沒有任何錯誤發生時，會和資料列位於結尾**資料錄集**。 設定**索引**所要的索引，然後再執行這個方法的屬性。  
  
 只與伺服器端資料指標支援這個方法。 搜尋不支援當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性值為**資料錄集**物件是**adUseClient**。  
  
 使用此方法時，才**資料錄集**物件已經開啟與[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值**adCmdTableDirect**。  
  
## <a name="filtering-the-results"></a>篩選結果  
 **尋找**方法限制搜尋範圍，以一個欄位的內容。 **搜尋**方法需要您具有索引，並具有其他限制也。 如果您必須搜尋不是索引的基礎的多個欄位，或如果您的提供者不支援索引，您可以使用來限制結果**篩選**屬性**資料錄集**物件。  
  
 使用**篩選**以選擇性地篩選出記錄中的屬性**資料錄集**物件。 將已篩選**資料錄集**會變成目前的資料指標，表示記錄，並符合**篩選**準則都無法使用**資料錄集**之前**篩選**已移除。 其他屬性會傳回目前的資料指標為基礎的值會受到影響，例如**AbsolutePosition**， **AbsolutePage**， **RecordCount**，和**PageCount**。 這是因為設定**篩選**為特定值的屬性會將目前的記錄移至第一筆記錄符合新值。  
  
 **篩選**屬性使用變數引數。 這個值表示使用三種方法之一**篩選**屬性： 準則字串**FilterGroupEnum**常數或書籤的陣列。 如需詳細資訊，請參閱本主題稍後的篩選條件字串，與常數，篩選和篩選利用書籤。  
  
> [!NOTE]
>  當您知道您想要選取的資料時，會開啟通常更有效率**資料錄集**搭配 SQL 陳述式有效地篩選結果集，而不是依賴**篩選**屬性。  
  
 若要移除的篩選**資料錄集**，使用**adFilterNone**常數。 設定**篩選**屬性設為零長度字串 ("") 已使用相同的效果**adFilterNone**常數。  
  
### <a name="filtering-with-a-criteria-string"></a>篩選條件字串  
 準則字串所組成的表單中的子句*FieldName 運算子值*(例如， `"LastName = 'Smith'"`)。 您可以藉由串連個別的定序子句建立複合子句**AND** (例如， `"LastName = 'Smith' AND FirstName = 'John'"`) 和**或者**(例如， `"LastName = 'Smith' OR LastName = 'Jones'"`)。 準則字串，請使用下列指導方針：  
  
-   *FieldName*必須是有效的欄位名稱從**資料錄集**。 如果欄位名稱包含空格，必須以方括號括住的名稱。  
  
-   *運算子*必須是下列其中之一：  **\<** ，  **>** ，  **\< =** ，  **>=**  **<>** ，  **=** ，或**像**。  
  
-   *值*是與您將會比較欄位值的值 (例如， `'Smith'`， `#8/24/95#`， `12.345`，或`$50.00`)。 字串中使用單引號 （'） 與井字符號 (`#`) 的日期。 數字，您可以使用小數位數、 貨幣符號和科學記號標記法。 如果*運算子*是**像**，*值*可以使用萬用字元。 只有星號 (\*) 和百分比符號 （%） 萬用字元所允許的字元，而且它們必須是字串中的最後一個字元。 *值*不可為 null。  
  
    > [!NOTE]
    >  若要在篩選中包含單引號 （'）*值*，使用兩個單引號來代表其中一個。 例如，若要篩選*O'Malley*，準則字串應該`"col1 = 'O''Malley'"`。 若要包含在開頭和結尾的篩選值單引號，請將字串括以井字號 （#）。 例如，若要篩選*'1'*，準則字串應該`"col1 = #'1'#"`。  
  
 沒有任何優先順序之間**AND**和**或**。 子句可加以群組括號內。 不過，您無法群組子句聯結**或**然後將群組加入 AND，與另一個子句，如下所示。  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 相反地，您建構此篩選條件，如下所示。  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 中**像**子句，您可以在開頭和結尾的模式中使用萬用字元 (例如， `LastName Like '*mit*'`) 或只在模式結尾 (比方說， `LastName Like 'Smit*'`)。  
  
### <a name="filtering-with-a-constant"></a>篩選與常數  
 下列常數是可用於篩選**資料錄集**。  
  
|常數|描述|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|篩選器來檢視記錄，最後會受到**刪除**，**重新同步處理**， **UpdateBatch**，或**CancelBatch**呼叫。|  
|**adFilterConflictingRecords**|檢視失敗，最後一個批次更新記錄的篩選條件。|  
|**adFilterFetchedRecords**|在目前的快取中檢視記錄的篩選器 — 也就是從資料庫擷取記錄的最後一個呼叫的結果。|  
|**adFilterNone**|移除目前的篩選條件，並還原所有記錄的檢視。|  
|**adFilterPendingRecords**|篩選器來檢視只記錄已變更但尚未傳送到伺服器。 僅適用於批次更新模式。|  
  
 篩選條件常數更輕鬆地解決個別記錄的衝突，在批次更新模式，可讓您檢視，例如，只有那些記錄期間受到影響時最後一個**UpdateBatch**方法呼叫中所示下列範例。  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>使用書籤篩選  
 最後，您可以傳遞 variant 的陣列的書籤，以便**篩選**屬性。 產生的資料指標會包含其書籤傳遞給屬性的記錄。 下列程式碼範例建立的書籤陣列中的記錄從**資料錄集**具有"B" *ProductName*欄位。 接著，將陣列**篩選**資訊產生已篩選屬性，並顯示**資料錄集**。  
  
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
  
## <a name="creating-a-clone-of-a-recordset"></a>建立複製的資料錄集  
 使用**複製**方法來建立多個重複**資料錄集**物件，特別是如果您想要維護多個目前記錄的記錄組中。 使用**複製**方法會更有效率，比建立並開啟新**資料錄集**具有相同的定義與原始物件。  
  
 新建立複製品的目前記錄原本設定為第一筆記錄。 在複製目前的記錄指標**資料錄集**未同步處理與原始 （或相反）。 您可以在每個獨立巡覽**資料錄集**。  
  
 您對其中一個變更**資料錄集**物件中會顯示所有它的複製品，不論資料指標類型。 不過，之後您執行[Requery](../../../ado/reference/ado-api/requery-method.md)原始**資料錄集**，複製程式碼將不再同步處理至原始。  
  
 關閉原始**資料錄集**不會關閉它的複本，也不會關閉複本關閉原始或任何其他複本。  
  
 您可以複製**資料錄集**物件它是否支援書籤。 書籤值是可互換。也就是從某個書籤參考**資料錄集**物件參照到任何其複製品中的相同記錄。
