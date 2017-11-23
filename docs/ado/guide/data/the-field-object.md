---
title: "Field 物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ecd2382d15536a5c2ebd2b2098c89c41c78ba1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="the-field-object"></a>Field 物件
每個**欄位**物件通常會對應至資料庫資料表中的資料行。 不過，**欄位**也可以代表一個指標到另一個**資料錄集**，稱為章節。 例外狀況，例如章節資料行，將稍後在本指南涵蓋。  
  
 使用**值**屬性**欄位**設定或傳回目前的記錄資料的物件。 依據其功能提供者會公開，某些集合、 方法或屬性的**欄位**物件可能無法使用。  
  
 使用集合、 方法和屬性的**欄位**物件，您可以執行下列：  
  
-   使用傳回的欄位名稱**名稱**屬性。  
  
-   檢視或變更欄位中的資料使用**值**屬性。 **值**是預設屬性**欄位**物件。  
  
-   使用傳回欄位的基本特性**類型**，**精確度**，和**NumericScale**屬性。  
  
-   傳回欄位的宣告的大小使用**DefinedSize**屬性。  
  
-   使用指定的欄位中傳回資料的實際大小**ActualSize**屬性。  
  
-   判斷指定的欄位是否支援何種類型的功能使用**屬性**屬性和**屬性**集合。  
  
-   管理包含長的二進位或長度的字元資料使用欄位的值**AppendChunk**和**GetChunk**方法。  
  
 解決在批次更新所使用的欄位值不一致的地方**OriginalValue**和**UnderlyingValue**屬性，如果提供者支援批次更新。  
  
## <a name="describing-a-field"></a>描述欄位  
 請遵循將的主題將討論的內容[欄位](../../../ado/reference/ado-api/field-object.md)物件，代表資訊會描述**欄位**物件本身 — 也就是關於欄位的中繼資料。 這項資訊可以用來判斷太多的結構描述**資料錄集**。 這些屬性包括**類型**， **DefinedSize**和**ActualSize**，**名稱**，和**NumericScale**和**精確度**。  
  
### <a name="discovering-the-data-type"></a>探索的資料類型  
 **類型**屬性會指出欄位的資料類型。 ADO 支援的列舉的常數所述的資料型別[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)中*ADO 程式設計人員參考*。  
  
 浮點數值類型，例如**adNumeric**，您可以取得詳細的資訊。 **NumericScale**屬性會指出要在小數點右邊的數字位數會用來代表的值**欄位**。 **精確度**屬性會指定用來代表值的數字的最大數目**欄位**。  
  
### <a name="determining-field-size"></a>決定欄位大小  
 使用**DefinedSize**屬性來判斷的資料容量**欄位**物件。  
  
 使用**ActualSize**屬性傳回的實際長度**欄位**物件的值。 針對所有欄位， **ActualSize**屬性是唯讀的。 如果 ADO 無法判斷長度的**欄位**物件的值**ActualSize**屬性會傳回**adUnknown**。  
  
 **DefinedSize**和**ActualSize**屬性有不同的用途。 例如，請考慮**欄位**物件宣告類型為**adVarChar**和**DefinedSize**屬性值為 50，其中包含單一字元。 **ActualSize**它所傳回的屬性值是單一字元的長度以位元組為單位。  
  
### <a name="determining-field-contents"></a>決定欄位內容  
 資料來源的資料行的識別碼由**名稱**屬性**欄位**。 **值**屬性**欄位**物件傳回或設定欄位的實際資料內容。 這是預設屬性。  
  
 若要變更欄位中的資料，設定**值**屬性等於正確類型的新值。 資料指標類型必須支援更新，若要變更欄位的內容。 資料庫驗證不是這裡在批次模式中，因此您必須檢查是否有錯誤，當您呼叫**UpdateBatch**這種情況。 某些提供者也支援之 ADO**欄位**物件的**UnderlyingValue**和**OriginalValue**屬性，以協助您解決衝突，當您嘗試以了解執行批次更新。 如需有關如何解決這類衝突的詳細資訊，請參閱[編輯資料](../../../ado/guide/data/editing-data.md)。  
  
> [!NOTE]
>  **資料錄集欄位**無法設定值，當新附加**欄位**至**資料錄集**。 相反地，新**欄位**可以附加至已關閉**資料錄集**。 然後在**資料錄集**必須是已開啟，並只然後可以將值指派給這些**欄位**。  
  
### <a name="getting-more-field-information"></a>取得欄位的詳細資訊  
 ADO 物件有兩種類型的屬性： 內建和動態。 此時，只有的內建屬性**欄位**物件已經討論過。  
  
 內建屬性是在 ADO 中實作並立即提供給任何這些屬性新物件，使用`MyObject.Property`語法。 它們不會顯示成**屬性**物件中的物件**屬性**集合。  
  
 動態屬性是由定義基礎資料提供者，而會出現在**屬性**適當 ADO 物件的集合。 例如，提供者特定的屬性可能表示如果**資料錄集**物件支援交易，或更新。 這些額外的屬性會顯示為**屬性**中的物件**資料錄集**物件的**屬性**集合。 動態屬性可以參考集合中，使用的語法只能透過`MyObject.Properties(0)`或`MyObject.Properties("Name")`。  
  
 您無法刪除任何一種屬性。  
  
 動態**屬性**物件都有自己的四個內建屬性：  
  
-   **名稱**屬性是一個字串，識別屬性。  
  
-   **類型**屬性是整數，指定屬性資料型別。  
  
-   **值**屬性是包含的屬性設定為 variant。 **值**是預設屬性**屬性**物件。  
  
-   **屬性**屬性是**長**值，指出提供者特定屬性的特性。  
  
 **屬性**集合**欄位**物件包含關於欄位的其他中繼資料。 這個集合的內容而有所不同，提供者。 下列程式碼範例會檢查**屬性**的範例集合**資料錄集**引入在此區段的開頭。 會先查看集合的內容。 此程式碼使用[OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，因此**屬性**集合包含該提供者的相關資訊。  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>處理二進位資料  
 使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法**欄位**填入長二進位或字元資料的物件。 在系統記憶體的限制狀況下，您可以使用**AppendChunk**方法來處理部分中，而不是完整的長值。  
  
 如果**adFldLong**位元**屬性**屬性**欄位**物件設定為**True**，您可以使用**AppendChunk**該欄位的方法。  
  
 第一個**AppendChunk**上呼叫**欄位**物件會將資料寫入欄位，並覆寫任何現有的資料。 後續**AppendChunk**呼叫加入至現有的資料。 如果您將資料附加到一個欄位，然後設定或讀取目前記錄中的另一個欄位的值，ADO 會假設您已完成將資料附加到第一個欄位。 如果您呼叫**AppendChunk**方法上的第一個欄位，ADO 會解譯為新的呼叫**AppendChunk**作業，並覆寫現有的資料。 存取其他欄位**資料錄集**不是複製程式碼的第一個物件**資料錄集**物件不會破壞**AppendChunk**作業。  
  
 使用**GetChunk**方法**欄位**擷取部分或所有長二進位或字元資料的物件。 在系統記憶體的限制狀況下，您可以使用**GetChunk**方法來操作部分，而不是完整的長值。  
  
 資料的**GetChunk**呼叫傳回指派給*變數*。 如果*大小*大於剩餘的資料， **GetChunk**方法傳回的剩餘資料沒有填補*變數*使用空格。 如果欄位是空的**GetChunk**方法會傳回 null 值。  
  
 每個後續**GetChunk**呼叫會擷取資料從何處開始先前**GetChunk**離開的呼叫。 不過，如果您從一個欄位中擷取資料，然後設定或讀取目前記錄中的另一個欄位的值，ADO 會假設您完成從第一個欄位中擷取資料。 如果您呼叫**GetChunk**方法上的第一個欄位，ADO 會解譯為新的呼叫**GetChunk**作業，並讀取資料的開頭開始。 存取其他欄位**資料錄集**不是複製程式碼的第一個物件**資料錄集**物件不會破壞**GetChunk**作業。  
  
 如果**adFldLong**位元**屬性**屬性**欄位**物件設定為**True**，您可以使用**GetChunk**該欄位的方法。  
  
 如果當您使用會有無目前記錄**GetChunk**或**AppendChunk**方法**欄位**物件，就會發生錯誤 3021 （無目前記錄）。  
  
 如需使用這些方法來操作二進位資料的範例，請參閱[AppendChunk 方法](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk 方法](../../../ado/reference/ado-api/getchunk-method-ado.md)中的範例*ADO 程式設計人員參考*。
