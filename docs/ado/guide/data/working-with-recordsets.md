---
description: 使用資料錄集
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
ms.openlocfilehash: 84f60e269bcd01bdacc7647f1498c588620f049e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452520"
---
# <a name="working-with-recordsets"></a>使用資料錄集
**記錄集**物件具有內建功能，可讓您重新排列結果集中的資料順序、根據您提供的準則來搜尋特定記錄，甚至使用索引來優化這些搜尋作業。 這些功能是否可供使用，取決於提供者，以及在某些情況下（例如 [Index](../../../ado/reference/ado-api/index-property.md) 屬性）（資料來源本身的結構）。  
  
## <a name="arranging-data"></a>排列資料  
 在 **記錄集中** 排序資料的最有效率方式通常是在用來傳回結果的 SQL 命令中指定 order by 子句。 不過，您可能必須在已經建立的 **記錄集中** 變更資料的順序。 您可以使用 **Sort** 屬性來建立資料列 **集** 之資料列的遍歷順序。 此外， **Filter** 屬性會決定當您遍歷資料列時可以存取哪些資料列。  
  
 **Sort**屬性會設定或傳回**字串**值，表示要排序之**記錄集中**的功能變數名稱。 每個名稱會以逗號分隔，並選擇性地在後面加上空格和關鍵字 **ASC** (，這會以遞增順序排序欄位) 或 **DESC** (以遞減順序排序欄位) 。 依預設，如果未指定關鍵字，則會以遞增順序排序欄位。  
  
 排序作業很有效率，因為資料不會實際重新排列，而是依索引所指定的順序來存取。  
  
 **Sort**屬性需要將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 如果索引不存在，就會為 **Sort** 屬性中指定的每個欄位建立暫存索引。  
  
 將 [ **排序** ] 屬性設定為空字串，會將資料列重設為其原始順序，並刪除暫存索引。 不會刪除現有的索引。  
  
 假設 **記錄集** 包含名為 *firstName*、 *middleInitial*和 *lastName*的三個欄位。 將 **Sort** 屬性設定為字串 " `lastName DESC, firstName ASC` "，這會依姓氏的遞減順序排序 **記錄集** ，然後依名字以遞增順序排序。 會忽略中間的初始。  
  
 排序準則字串中參考的欄位不可以命名為 "ASC" 或 "DESC"，因為這些名稱與關鍵字 **ASC** 和 **DESC**相衝突。 在傳回**記錄集**的查詢中使用**AS**關鍵字，為具有衝突名稱的欄位提供別名。  
  
 如需有關 **記錄集** 篩選的詳細資訊，請參閱本主題稍後的「篩選結果」。  
  
## <a name="finding-a-specific-record"></a>尋找特定記錄  
 ADO 提供 [尋找](../../../ado/reference/ado-api/find-method-ado.md) 和 [搜尋](../../../ado/reference/ado-api/seek-method.md) 方法，以尋找 **記錄集中**的特定記錄。 **Find**方法是由各種提供者所支援，但僅限於單一搜尋準則。 **Seek**方法支援搜尋多個準則，但許多提供者並不支援。  
  
 欄位上的索引可以大幅提升**Find**方法的效能，以及**記錄集**物件的**排序**和**篩選**屬性。 您可以藉由設定 [動態[優化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)] 屬性來建立**欄位**物件的內部索引。 當您將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**時，這個動態屬性會加入至**Field**物件的**Properties**集合中。 請記住，這是 ADO 的內部索引，您無法取得其存取權，或將它用於任何其他用途。 此外，此索引與**記錄集**物件的[index](../../../ado/reference/ado-api/index-property.md)屬性不同。  
  
 Find 方法會快速 **找** 出資料行中的值， (欄位) **記錄集**。 您可以使用**Optimize**屬性在資料行上建立索引，以頻繁地改善**Find**方法的速度。  
  
 **Find**方法會將您的搜尋限制為一個欄位的內容。 **Seek**方法需要您擁有索引，而且也有其他限制。 如果您必須搜尋不是索引基礎的多個欄位，或您的提供者不支援索引，您可以使用**記錄集**物件的**Filter**屬性來限制結果。  
  
### <a name="find"></a>Find  
 **Find**方法會搜尋**記錄集**，以找出符合指定準則的資料列。 您可以選擇性地指定搜尋的方向、開始的資料列，以及起始資料列的位移。 如果符合準則，就會在找到的記錄上設定目前的資料列位置。否則，此位置會設定為 **記錄集**的結束 (或開始) ，視搜尋方向而定。  
  
 只能針對準則指定單一資料行名稱。 換句話說，這個方法並不支援多行搜尋。  
  
 準則的比較運算子可以是 " **>** " (大於) 、"* * \<**" (less than), "=" (equal), "> =" (大於或等於) 、"<=" (小於或等於) 、"<>" (不等於) 或 "LIKE" (模式比對) 。  
  
 準則值可以是字串、浮點數或日期。 字串值以單引號分隔，或使用 "#" (數位記號) 標記 (例如，"state = ' WA '" 或 "state = #WA #" ) 。 日期值會以 "#" 分隔 (數位記號) 標記 (例如 "start_date > #7/22/97 #" ) 。  
  
 如果比較運算子「贊」，則字串值可以包含星號 ( * ) ，以找出一個或多個字元或子字串的出現次數。 例如，「州（州）」會 \* 符合 Maine 和麻塞諸塞州。 您也可以使用前置和尾端星號來尋找包含在值內的子字串。 例如，「as」之類的「狀態」會 \* \* 符合阿拉斯加、Arkansas 和麻塞諸塞州。  
  
 星號只能用在準則字串的結尾，或同時在準則字串的開頭和結尾，如先前所示。 您無法使用星號做為前置萬用字元 ( ' * str ' ) 或內嵌萬用字元 ( 的 \* r ' ) 。 這會導致錯誤。  
  
### <a name="seek-and-index"></a>搜尋和索引  
 如果基礎提供者支援**記錄集**物件上的索引，請搭配**Index**屬性使用**Seek**方法。 使用 [支援](../../../ado/reference/ado-api/supports-method.md)** (adSeek) ** 方法來判斷基礎提供者是否支援 **搜尋**，並且 **支援 (adIndex) ** 方法來判斷提供者是否支援索引。  (例如， [Microsoft Jet 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) 支援 **搜尋** 和 **索引**。 )   
  
 如果 **Seek** 找不到所需的資料列，就不會發生錯誤，而且資料列會定位於 **記錄集**的結尾。 執行此方法之前，請先將 **索引** 屬性設定為所需的索引。  
  
 只有伺服器端資料指標才支援這個方法。 當**記錄集**物件的[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性值為**adUseClient**時，不支援搜尋。  
  
 只有在使用**adCmdTableDirect**的[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值開啟**記錄集**物件時，才能使用這個方法。  
  
## <a name="filtering-the-results"></a>篩選結果  
 **Find**方法會將您的搜尋限制為一個欄位的內容。 **Seek**方法需要您擁有索引，而且也有其他限制。 如果您必須搜尋不是索引基礎的多個欄位，或您的提供者不支援索引，您可以使用**記錄集**物件的**Filter**屬性來限制結果。  
  
 使用 **Filter** 屬性可選擇性地顯示 **記錄集** 物件中的記錄。 篩選的**記錄集會**變成目前的資料指標，這表示不符合**篩選**準則的記錄在移除**篩選**之前無法在**記錄集中**使用。 根據目前資料指標傳回值的其他屬性會受到影響，例如 **AbsolutePosition**、 **AbsolutePage**、 **RecordCount**和 **PageCount**。 這是因為將 **篩選** 屬性設定為特定值，會將目前的記錄移至符合新值的第一筆記錄。  
  
 **Filter**屬性採用 variant 引數。 此值代表使用 **Filter** 屬性的三種方法之一：準則字串、 **FilterGroupEnum** 常數或書簽的陣列。 如需詳細資訊，請參閱本主題稍後的使用條件字串篩選、使用常數進行篩選，以及使用書簽進行篩選。  
  
> [!NOTE]
>  當您知道想要選取的資料時，使用可有效篩選結果集的 SQL 語句來開啟 **記錄集** ，而不是依賴 **Filter** 屬性，通常會更有效率。  
  
 若要從 **記錄集**移除篩選，請使用 **adFilterNone** 常數。 將 **Filter** 屬性設定為長度為零的字串 ( "" ) 與使用 **adFilterNone** 常數的效果相同。  
  
### <a name="filtering-with-a-criteria-string"></a>使用準則字串篩選  
 準則字串是由格式為 *FieldName 運算子值* 的子句所組成 (例如 `"LastName = 'Smith'"`) 。 您可以藉由串連個別子句 **和和** (（例如 `"LastName = 'Smith' AND FirstName = 'John'"`) 和 **或** (例如) ）來建立複合子句 `"LastName = 'Smith' OR LastName = 'Jones'"` 。 使用準則字串的下列指導方針：  
  
-   *FieldName* 必須是 **記錄集中**有效的功能變數名稱。 如果功能變數名稱包含空格，您必須將名稱括在方括弧中。  
  
-   *運算子* 必須是下列其中一項： **\<**, **>** 、 **\<=**, **>=** 、 **<>** 、 **=** 或 **等**。  
  
-   *值* 是用來比較域值 (的值，例如、、、 `'Smith'` `#8/24/95#` `12.345` 或 `$50.00`) 。 使用單引號 ( ' ) 搭配字串和井字元號 (`#`) 日期。 若為數字，您可以使用小數點、貨幣符號和科學記號標記法。 如果 *運算子* 是 **LIKE**，則 *值* 可以使用萬用字元。 只允許星號 (\*) 和百分比符號 (% ) 萬用字元，且必須是字串中的最後一個字元。 *值* 不可為 null。  
  
    > [!NOTE]
    >  若要在篩選 *值*中加入單引號 ( ' ) ，請使用兩個單引號來表示一個。 例如，若要篩選 *O'Malley*，準則字串應該是 `"col1 = 'O''Malley'"` 。 若要在篩選值的開頭和結尾加上單引號，請以井字型大小 ( # ) 括住字串。 例如，若要篩選 *' 1 '*，準則字串應該是 `"col1 = #'1'#"` 。  
  
 **And**和**OR**之間沒有任何優先順序。 子句可以在括弧內分組。 不過，您不能將由 **或** 聯結的子句群組在一起，然後使用和將群組聯結至另一個子句，如下所示。  
  
```  
(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'  
```  
  
 相反地，您會依照下列方式來建立此篩選器。  
  
```  
(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')  
```  
  
 在 **LIKE** 子句中，您可以在模式的開頭和結尾使用萬用字元 (例如， `LastName Like '*mit*'`) ，或只在模式的結尾處 (例如 `LastName Like 'Smit*'`) 。  
  
### <a name="filtering-with-a-constant"></a>使用常數進行篩選  
 下列常數可用於篩選 **記錄集**。  
  
|持續性|描述|  
|--------------|-----------------|  
|**adFilterAffectedRecords**|僅用於查看由上次 **刪除**、重新 **同步**、 **UpdateBatch**或 **CancelBatch** 呼叫所影響之記錄的篩選準則。|  
|**adFilterConflictingRecords**|用來查看上次批次更新失敗記錄的篩選準則。|  
|**adFilterFetchedRecords**|用來查看目前快取中記錄的篩選器，也就是上次呼叫從資料庫取出記錄的結果。|  
|**adFilterNone**|移除目前的篩選，並還原所有記錄以進行查看。|  
|**adFilterPendingRecords**|僅用於查看已變更但尚未傳送至伺服器之記錄的篩選準則。 僅適用于批次更新模式。|  
  
 篩選準則常數讓您能夠在批次更新模式中，輕鬆地解決個別記錄衝突，例如，您可以只查看在最後一個 **UpdateBatch** 方法呼叫期間受影響的記錄，如下列範例所示。  
  
 `Attribute VB_Name = "modExaminingData"`  
  
### <a name="filtering-with-bookmarks"></a>使用書簽進行篩選  
 最後，您可以將書簽的 variant 陣列傳遞至 **篩選** 屬性。 產生的資料指標只會包含已傳遞至屬性之書簽的記錄。 下列程式碼範例會從記錄集的記錄中建立書簽的陣列，此記錄 **集會** 在 *ProductName* 欄位中有 "B"。 然後，它會將陣列傳遞至 **篩選** 屬性，並顯示所產生之已篩選 **記錄集**的相關資訊。  
  
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
  
## <a name="creating-a-clone-of-a-recordset"></a>建立記錄集的複本  
 您可以使用 **Clone** 方法來建立多個重複的 **記錄集** 物件，尤其是如果您想要在一組指定的記錄中維護一個以上的目前記錄。 使用 **Clone** 方法比建立和開啟具有與原始相同之定義的新 **記錄集** 物件更有效率。  
  
 新建立之複製的目前記錄原本是設定為第一筆記錄。 複製的 **記錄集** 內目前的記錄指標不會與原始的或反向同步處理。 您可以在每個 **記錄集**內獨立導覽。  
  
 您對一個 **記錄集** 物件所做的變更，不論資料指標類型為何，都可以在其所有複製中看到。 不過，在原始記錄集上執行重新 [查詢](../../../ado/reference/ado-api/requery-method.md) 之後，複製就不會再同步處理至原始 **記錄集**。  
  
 關閉原始 **記錄集** 並不會關閉其複本，也不會關閉複製以關閉原始或任何其他複本。  
  
 只有在支援書簽時，才可以複製 **記錄集** 物件。 書簽值是可互換的;也就是說，來自一個 **記錄集** 物件的書簽參考會參考其任何複製中的相同記錄。
