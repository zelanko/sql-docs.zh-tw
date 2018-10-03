---
title: Field 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc75b9a7ab93e3157d6594be15c0b2cc36456415
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726156"
---
# <a name="the-field-object"></a>Field 物件
每個**欄位**物件通常會對應至資料庫資料表中的資料行。 不過，**欄位**也可以代表指標到另一個**資料錄集**，呼叫一章。 例外狀況，例如章節資料行，將本指南稍後會說明。  
  
 使用**值**屬性**欄位**設定或傳回目前的記錄資料的物件。 某些集合、 方法或屬性會提供者依據其功能的公開**欄位**物件可能無法使用。  
  
 使用集合、 方法和屬性的**欄位**物件時，您可以執行下列動作：  
  
-   使用傳回的欄位名稱**名稱**屬性。  
  
-   檢視或變更所使用的欄位中的資料**值**屬性。 **值**是預設屬性**欄位**物件。  
  
-   使用傳回欄位的基本特性**型別**，**有效位數**，並**NumericScale**屬性。  
  
-   使用傳回的欄位宣告的大小**DefinedSize**屬性。  
  
-   使用指定的欄位中傳回資料的實際大小**ActualSize**屬性。  
  
-   判斷哪些類型的功能支援使用指定的欄位**屬性**屬性並**屬性**集合。  
  
-   管理使用包含長的二進位或長度字元資料欄位的值**AppendChunk**並**GetChunk**方法。  
  
 解決在批次更新使用的欄位值不一致的地方**OriginalValue**並**UnderlyingValue**屬性，如果提供者支援批次更新。  
  
## <a name="describing-a-field"></a>描述欄位  
 請遵循將的主題將討論的屬性[欄位](../../../ado/reference/ado-api/field-object.md)代表描述資訊的物件**欄位**物件本身，也就是相關欄位的中繼資料。 這項資訊可用來判斷太多的結構描述**資料錄集**。 這些屬性包括**型別**， **DefinedSize**並**ActualSize**，**名稱**，和**NumericScale**並**有效位數**。  
  
### <a name="discovering-the-data-type"></a>探索的資料類型  
 **型別**屬性指出欄位的資料類型。 ADO 支援的列舉的常數所述的資料型別[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)中*ADO 程式設計人員參考*。  
  
 浮點數值型別這類**adNumeric**，您可以取得更多的資訊。 **NumericScale**屬性會指出小數點右邊的位數數目會用來代表值**欄位**。 **有效位數**屬性會指定用來代表值的數字的最大數目**欄位**。  
  
### <a name="determining-field-size"></a>判斷欄位大小  
 使用**DefinedSize**屬性來判斷的資料容量**欄位**物件。  
  
 使用**ActualSize**屬性傳回的實際長度**欄位**物件的值。 所有欄位，如**ActualSize**屬性是唯讀的。 如果 ADO 無法判斷長度**欄位**物件的值**ActualSize**屬性會傳回**adUnknown**。  
  
 **DefinedSize**並**ActualSize**屬性有不同的用途。 例如，請考慮**欄位**宣告類型的物件**adVarChar**並**DefinedSize**屬性值為 50，其中包含單一字元。 **ActualSize**它所傳回的屬性值是單一字元的長度以位元組為單位。  
  
### <a name="determining-field-contents"></a>判斷欄位內容  
 資料來源的資料行的識別碼由**名稱**屬性**欄位**。 **值**屬性**欄位**物件傳回或設定欄位的實際資料內容。 這是預設屬性。  
  
 若要變更欄位中的資料，請設定**值**屬性等於正確類型的新值。 資料指標類型必須支援更新，若要變更欄位的內容。 資料庫驗證不是此處在批次模式中，因此您必須檢查是否有錯誤，當您呼叫**UpdateBatch**這種情況。 某些提供者也支援之 ADO**欄位**物件的**UnderlyingValue**並**OriginalValue**可協助您解決衝突，當您嘗試將屬性執行批次更新。 如需有關如何解決這類衝突的詳細資訊，請參閱 <<c0> [ 編輯資料](../../../ado/guide/data/editing-data.md)。  
  
> [!NOTE]
>  **資料錄集欄位**無法設定值，當新附加**欄位**要**資料錄集**。 相反地，新**欄位**您可以附加至已關閉**資料錄集**。 然後**Recordset**必須是已開啟，並只然後可以將值指派給這些**欄位**。  
  
### <a name="getting-more-field-information"></a>取得欄位的詳細資訊  
 ADO 物件有兩種類型的屬性： 內建和動態。 到目前為止的內建屬性**欄位**物件已經討論過。  
  
 內建屬性可讓您為這些屬性，在 ADO 中實作和立即提供給任何新物件，使用`MyObject.Property`語法。 它們不會出現**屬性**物件中的物件**屬性**集合。  
  
 動態屬性由基礎資料提供者所定義，並會出現在**屬性**適當的 ADO 物件的集合。 例如，提供者特有的屬性可能表示如果**資料錄集**物件支援交易，或更新。 這些額外的屬性會成為**屬性**中的物件**Recordset**物件的**屬性**集合。 動態屬性可以參考只能透過集合中，使用語法`MyObject.Properties(0)`或`MyObject.Properties("Name")`。  
  
 您無法刪除屬性的其中一種。  
  
 動態**屬性**物件都有自己的四個內建的屬性：  
  
-   **名稱**屬性是字串，識別屬性。  
  
-   **型別**屬性是一個整數，指定屬性資料型別。  
  
-   **值**屬性是變化，其中包含的屬性設定。 **值**是預設屬性，如**屬性**物件。  
  
-   **屬性**屬性是**長**值，指出屬性提供者特有的特性。  
  
 **屬性**收集**欄位**物件包含關於欄位的其他中繼資料。 此集合的內容而有所不同，提供者。 下列程式碼範例會檢查**屬性**的範例集合**資料錄集**導入在這一節的開頭。 它首先會查看集合的內容。 此程式碼會使用[OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，因此**屬性**集合包含該提供者的相關資訊。  
  
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
 使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法**欄位**填入長二進位或字元資料的物件。 在其中的系統記憶體是有限的情況下，您可以使用**AppendChunk**方法來操作部分，而不是完整的長值。  
  
 如果**adFldLong**位元**屬性**屬性**欄位**物件設定為**True**，您可以使用**AppendChunk**該欄位的方法。  
  
 第一個**AppendChunk**上呼叫**欄位**物件會將資料寫入欄位中，覆寫任何現有的資料。 後續**AppendChunk**呼叫新增至現有的資料。 如果您將資料附加到一個欄位，然後設定或讀取目前的記錄中的另一個欄位的值，ADO 會假設您已完成將資料附加到第一個欄位。 如果您呼叫**AppendChunk**方法的第一個欄位，ADO 會解譯為新的呼叫**AppendChunk**作業，並覆寫現有的資料。 存取其他欄位**Recordset**不是複製程式碼的第一個物件**資料錄集**物件並不會影響**AppendChunk**作業。  
  
 使用**GetChunk**方法**欄位**擷取部分或所有長二進位或字元資料的物件。 在其中的系統記憶體是有限的情況下，您可以使用**GetChunk**方法來操作部分，而不是完整的長值。  
  
 資料可**GetChunk**呼叫會傳回指派給*變數*。 如果*大小*大於剩餘的資料， **GetChunk**方法會傳回只剩餘的資料沒有填補*變數*空白空間。 如果欄位是空的**GetChunk**方法會傳回 null 值。  
  
 每個後續**GetChunk**呼叫會擷取從何處開始的資料先前**GetChunk**離開的呼叫。 不過，如果您會擷取一個欄位的資料，然後設定或讀取目前的記錄中的另一個欄位的值，ADO 會假設您已完成擷取第一個欄位的資料。 如果您呼叫**GetChunk**方法的第一個欄位，ADO 會解譯為新的呼叫**GetChunk**作業，並讀取資料的開頭開始。 存取其他欄位**Recordset**不是複製程式碼的第一個物件**資料錄集**物件並不會影響**GetChunk**作業。  
  
 如果**adFldLong**位元**屬性**屬性**欄位**物件設定為**True**，您可以使用**GetChunk**該欄位的方法。  
  
 如果當您使用會有任何目前的資料錄**GetChunk**或是**AppendChunk**方法**欄位**物件時，就會發生錯誤 3021 （沒有目前的記錄）。  
  
 如需使用這些方法來操作二進位資料的範例，請參閱 < [AppendChunk 方法](../../../ado/reference/ado-api/appendchunk-method-ado.md)並[GetChunk 方法](../../../ado/reference/ado-api/getchunk-method-ado.md)中的範例*ADO 程式設計人員參考*。
