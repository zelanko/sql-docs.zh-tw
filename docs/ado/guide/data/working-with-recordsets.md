---
title: 使用記錄集 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 07f970dd557d381280f5a9dbdd52eb015de0df75
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748335"
---
# <a name="working-with-recordsets"></a>使用資料錄集
**記錄集**物件具有內建功能，可讓您重新排列結果集中的資料順序、根據您所提供的準則來搜尋特定記錄，甚至使用索引來優化這些搜尋作業。 這些功能是否可供使用，取決於提供者，以及在某些情況下（例如[索引](../../../ado/reference/ado-api/index-property.md)屬性的結構），也就是資料來源本身的結構。  
  
## <a name="arranging-data"></a>排列資料  
 排序**記錄集中**資料最有效率的方式，是在用來將結果傳回給它的 SQL 命令中指定 order by 子句。 不過，您可能必須變更已建立之**記錄集中**的資料順序。 您可以使用**Sort**屬性來建立資料列**集**的遍歷順序。 此外， **Filter**屬性會決定在遍歷資料列時，可以存取哪些資料列。  
  
 **Sort**屬性會設定或傳回**字串**值，表示要排序之**記錄集中**的功能變數名稱。 每個名稱都以逗號分隔，並選擇性地後面加上空格和關鍵字**ASC** （以遞增順序排序欄位）或**DESC** （以遞減順序排序欄位）。 根據預設，如果未指定關鍵字，則會以遞增順序排序欄位。  
  
 排序作業很有效率，因為資料不會實體地重新排列，而是以索引所指定的順序來存取。  
  
 **Sort**屬性需要將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 如果索引不存在，就會為**Sort**屬性中指定的每個欄位建立暫存索引。  
  
 將**排序**屬性設定為空字串，會將資料列重設為其原始順序，並刪除暫存索引。 將不會刪除現有的索引。  
  
 假設**記錄集**包含三個名*為 firstName*、 *middleInitial*和*lastName*的欄位。 將**Sort**屬性設定為字串 " `lastName DESC, firstName ASC` "，這會依姓氏以遞減的順序排序**記錄集**，然後依名字以遞增順序排列。 會忽略中間的初始。  
  
 排序準則字串中參考的欄位不能命名為 "ASC" 或 "DESC"，因為這些名稱與關鍵字**ASC**和**DESC**衝突。 在傳回**記錄集**的查詢中，使用**AS**關鍵字，為具有衝突名稱的欄位提供別名。  
  
 如需有關**記錄集**篩選的詳細資訊，請參閱本主題稍後的「篩選結果」。  
  
## <a name="finding-a-specific-record"></a>尋找特定記錄  
 ADO 提供[尋找](../../../ado/reference/ado-api/find-method-ado.md)和[尋找](../../../ado/reference/ado-api/seek-method.md)方法，以便尋找**記錄集中**的特定記錄。 **Find**方法受到各種提供者的支援，但僅限於單一搜尋條件。 **Seek**方法支援搜尋多個條件，但許多提供者都不支援。  
  
 欄位的索引可以大幅提升**Find**方法的效能，以及**排序**和**篩選****記錄集**物件的屬性。 您可以藉由設定**欄位**物件的動態[優化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)屬性來建立其內部索引。 當您將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**時，這個動態屬性會加入至**Field**物件的**Properties**集合中。 請記住，這是 ADO 內部的索引，您無法取得它的存取權，或將其用於其他用途。 此外，此索引與**記錄集**物件的[index](../../../ado/reference/ado-api/index-property.md)屬性不同。  
  
 **Find**方法會快速地在**記錄集**的資料行（欄位）中尋找值。 您可以使用 [**優化**] 屬性在資料行上建立索引，藉此提升資料行的**Find**方法速度。  
  
 **Find**方法會將您的搜尋限制為一個欄位的內容。 **搜尋**方法需要您擁有索引，而且也有其他限制。 如果您必須搜尋不是索引基礎的多個欄位，或如果您的提供者不支援索引，您可以使用**Recordset**物件的**Filter**屬性來限制結果。  
  
### <a name="find"></a>尋找  
 **Find**方法會搜尋**記錄集**，尋找符合指定之準則的資料列。 您可以選擇性地指定搜尋的方向、起始資料列，以及起始資料列的位移。 如果符合條件，就會在找到的記錄上設定目前的資料列位置。否則，視搜尋方向而定，位置會設定為**記錄集**的結束（或開始）。  
  
 只能為準則指定單一資料行名稱。 換句話說，這個方法不支援多重列搜尋。  
  
 準則的比較運算子可以是 " **>** " （大於）、" **\<** " （小於）、"=" （等於）、">=" （大於或等於）、"<=" （小於或等於）、"<>" （不等於）或 "LIKE" （模式比對）。  
  
 準則值可以是字串、浮點數或日期。 字串值會以單引號或 "#" （數位記號）標記分隔（例如，"state = ' WA '" 或 "state = #WA #"）。 日期值會以 "#" （數位記號）標記分隔（例如，"start_date > #7/22/97 #"）。  
  
 如果比較運算子是 "like"，則字串值可以包含星號（*），以找出一或多個出現的任何字元或子字串。 例如，「像是 ' m '」的狀態會 \* 符合 Maine 和麻塞諸塞州。 您也可以使用開頭和尾端的星號來尋找包含在值內的子字串。 例如，「如 ' as '」之類的狀態會 \* \* 符合阿拉斯加、Arkansas 和麻塞諸塞州。  
  
 星號只能用在準則字串的結尾，或同時在準則字串的開頭和結尾，如先前所示。 您不能使用星號做為前導萬用字元（' * str '）或內嵌萬用字元（的 \* r '）。 這會造成錯誤。  
  
### <a name="seek-and-index"></a>搜尋和索引  
 如果基礎提供者支援**記錄集**物件上的索引，請搭配使用**Seek**方法與**Index**屬性。 使用[支援](../../../ado/reference/ado-api/supports-method.md)**（adSeek）** 方法來判斷基礎提供者是否支援**搜尋**，以及**支援（adIndex）** 方法，以判斷提供者是否支援索引。 （例如， [Microsoft Jet 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)支援**搜尋**和**索引**）。  
  
 如果 [**搜尋**] 找不到所需的資料列，則不會發生錯誤，且資料列位於**記錄集**的結尾。 執行此方法之前，請先將**index**屬性設為所需的索引。  
  
 只有伺服器端資料指標才支援這個方法。 當**記錄集**物件的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性值為**adUseClient**時，不支援搜尋。  
  
 只有在以**adCmdTableDirect**的[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值開啟**記錄集**物件時，才可以使用這個方法。  
  
## <a name="filtering-the-results"></a>篩選結果  
 **Find**方法會將您的搜尋限制為一個欄位的內容。 **搜尋**方法需要您擁有索引，而且也有其他限制。 如果您必須搜尋不是索引基礎的多個欄位，或如果您的提供者不支援索引，您可以使用**Recordset**物件的**Filter**屬性來限制結果。  
  
 使用 [**篩選**] 屬性可選擇性地在**記錄集**物件中顯示記錄。 篩選的**記錄集會**變成目前的資料指標，這表示不符合**篩選**準則的記錄在移除**篩選器**之前，都無法在**記錄集中**使用。 根據目前資料指標傳回值的其他屬性會受到影響，例如**AbsolutePosition**、 **AbsolutePage**、 **RecordCount**和**PageCount**。 這是因為將**篩選**屬性設定為特定的值，會將目前的記錄移至符合新值的第一筆記錄。  
  
 **Filter**屬性會接受 variant 引數。 此值代表使用**Filter**屬性的三種方法之一：準則字串、 **FilterGroupEnum**常數或書簽陣列。 如需詳細資訊，請參閱本主題稍後的使用準則字串進行篩選、使用常數進行篩選，以及使用書簽進行篩選。  
  
> [!NOTE]
>  當您知道想要選取的資料時，使用可有效篩選結果集的 SQL 語句來開啟**記錄集**通常會更有效率，而不是依賴**篩選**屬性。  
  
 若要從**記錄集**移除篩選，請使用**adFilterNone**常數。 將**篩選**屬性設定為長度為零的字串（""）與使用**adFilterNone**常數的效果相同。  
  
### <a name="filtering-with-a-criteria-string"></a>使用準則字串進行篩選  
 準則字串是由子句所組成，其格式為*FieldName Operator 值*（例如 `"LastName = 'Smith'"` ）。 您可以串連個別子句與**和**（例如， `"LastName = 'Smith' AND FirstName = 'John'"` ）和**或**（例如，）來建立複合子句 `"LastName = 'Smith' OR LastName = 'Jones'"` 。 使用準則字串的下列指導方針：  
  
-   *FieldName*必須是**記錄集**的有效功能變數名稱。 如果功能變數名稱包含空格，您必須將名稱括在方括弧中。  
  
-   *運算子*必須是下列其中一項： **\<** 、 **>** 、 **\<=** 、 **>=** 、 **<>** 、 **=** 或**LIKE**。  
  
-   *Value*是您將用來比較域值的值（例如、、 `'Smith'` `#8/24/95#` `12.345` 或 `$50.00` ）。 搭配字串使用單引號（'）和以日期加上井字型大小（ `#` ）。 若為數字，您可以使用小數點、貨幣符號和科學標記法。 如果*運算子*是**LIKE**，則*Value*可以使用萬用字元。 只有星號（ \* ）和百分比符號（%）允許使用萬用字元，而且這些字元必須是字串中的最後一個字元。 *值*不可以是 null。  
  
    > [!NOTE]
    >  若要在篩選*值*中加入單引號（'），請使用兩個單引號來表示一個。 例如，若要篩選*O'Malley*，準則字串應該是 `"col1 = 'O''Malley'"` 。 若要在篩選值的開頭和結尾加上單引號，請以井字型大小（#）括住字串。 例如，若要篩選 *' 1 '*，準則字串應該是 `"col1 = #'1'#"` 。  
  
 **和**和**或**之間沒有任何優先順序。 子句可以在括弧內分組。 不過，您無法將**或**所聯結的子句分組，然後使用和將群組聯結至另一個子句，如下所示。  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 相反地，您會依照下列方式來建立此篩選器。  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 在**LIKE**子句中，您可以在模式的開頭和結尾使用萬用字元（例如， `LastName Like '*mit*'` ），或只在模式結尾（例如 `LastName Like 'Smit*'` ）。  
  
### <a name="filtering-with-a-constant"></a>使用常數進行篩選  
 下列常數適用于篩選**記錄集**。  
  
|持續性|描述|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|僅用於查看上次**刪除**、重新**同步**、 **UpdateBatch**或**CancelBatch**呼叫所影響之記錄的篩選準則。|  
|**adFilterConflictingRecords**|用於查看上次批次更新失敗記錄的篩選準則。|  
|**adFilterFetchedRecords**|用來在目前的快取中查看記錄的篩選-也就是最後一次呼叫從資料庫取得記錄的結果。|  
|**adFilterNone**|移除目前的篩選準則，並還原所有記錄以進行查看。|  
|**adFilterPendingRecords**|僅用於查看已變更但尚未傳送到伺服器之記錄的篩選。 僅適用于批次更新模式。|  
  
 篩選常數可讓您只查看在最後一個**UpdateBatch**方法呼叫期間受到影響的記錄，讓您更輕鬆地解決批次更新模式中的個別記錄衝突，如下列範例所示。  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>使用書簽進行篩選  
 最後，您可以將書簽的 variant 陣列傳遞至**Filter**屬性。 產生的資料指標只會包含已將書簽傳入屬性的記錄。 下列程式碼範例會從在 [ *ProductName* ] 欄位中有 "B"**的記錄中**，建立書簽的陣列。 然後，它會將陣列傳遞至**Filter**屬性，並顯示產生之已篩選**記錄集**的相關資訊。  
  
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
  
## <a name="creating-a-clone-of-a-recordset"></a>建立記錄集的複製  
 使用**Clone**方法來建立多個重複的**記錄集**物件，特別是當您想要在一組指定的記錄中維護一筆以上的目前記錄時。 使用**Clone**方法比建立和開啟新的**記錄集**物件的方式更有效率，其定義與原始的相同。  
  
 新建立之複製的目前記錄最初會設定為第一筆記錄。 複製的**記錄集中**目前的記錄指標不會與原始的（反之亦然）同步處理。 您可以在每個**記錄集**內獨立導覽。  
  
 無論資料指標類型為何，您對一個**記錄集**物件所做的變更都會顯示在所有的複本中。 不過，在原始**記錄集**上執行重新[查詢](../../../ado/reference/ado-api/requery-method.md)之後，複本將不會再同步處理至原始的。  
  
 關閉原始的**記錄集**並不會關閉其複本，也不會關閉複製，以關閉原始或任何其他複本。  
  
 只有在支援書簽時，才可以複製**記錄集**物件。 書簽值是可互換的;也就是說，來自一個**記錄集**物件的書簽參考是指其任何複製中的相同記錄。
