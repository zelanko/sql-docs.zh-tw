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
ms.openlocfilehash: 80e6576b236db44452c4e89b1d8f3bb8976ab120
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923988"
---
# <a name="the-field-object"></a>Field 物件
每個**Field**物件通常會對應至資料庫資料表中的資料行。 不過，**欄位**也可以代表指向另一個**記錄集**的指標，稱為「章節」。 本指南稍後將會涵蓋如章節專欄的例外狀況。  
  
 使用 [**欄位**物件] 的 [**值**] 屬性來設定或傳回目前記錄的資料。 視提供者公開的功能而定，可能無法使用**欄位**物件的某些集合、方法或屬性。  
  
 使用**Field**物件的集合、方法和屬性，您可以執行下列動作：  
  
-   使用**name**屬性來傳回欄位的名稱。  
  
-   使用**Value**屬性來查看或變更欄位中的資料。 **Value**是**Field**物件的預設屬性。  
  
-   使用**Type**、 **Precision**和**NumericScale**屬性，傳回欄位的基本特性。  
  
-   使用**DefinedSize**屬性傳回欄位的宣告大小。  
  
-   使用**ActualSize**屬性，傳回給定欄位中的資料實際大小。  
  
-   使用**Attributes**屬性和**Properties**集合，判斷給定欄位支援哪些類型的功能。  
  
-   使用**AppendChunk**和**GetChunk**方法，操作包含長二進位或長字元資料的欄位值。  
  
 如果提供者支援批次更新，請使用**OriginalValue**和**UnderlyingValue**屬性，在批次更新期間解決域值不一致的情況。  
  
## <a name="describing-a-field"></a>描述欄位  
 接下來的主題將討論[field](../../../ado/reference/ado-api/field-object.md)物件的屬性，其代表描述**欄位**物件本身的資訊，也就是欄位的相關中繼資料。 這項資訊可以用來判斷有關**記錄集**架構的內容。 這些屬性包括**Type**、 **DefinedSize**和**ActualSize**、 **Name**、 **NumericScale**和**Precision**。  
  
### <a name="discovering-the-data-type"></a>探索資料類型  
 **Type**屬性會指出欄位的資料類型。 Ado 所支援的資料型別列舉常數[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)在 ado 程式設計*人員參考*中。  
  
 如需浮點數數值型別（例如**adNumeric**），您可以取得詳細資訊。 **NumericScale**屬性會指出要使用小數點右邊多少位數來表示**欄位**的值。 **Precision**屬性會指定用來表示**欄位**值的最大位數。  
  
### <a name="determining-field-size"></a>判斷欄位大小  
 使用**DefinedSize**屬性來判斷**欄位**物件的資料容量。  
  
 使用**ActualSize**屬性可傳回**欄位**物件值的實際長度。 對於所有欄位而言， **ActualSize**屬性都是唯讀的。 如果 ADO 無法判斷**欄位**物件值的長度， **ActualSize**屬性會傳回**adUnknown**。  
  
 **DefinedSize**和**ActualSize**屬性有不同的用途。 例如，假設**欄位**物件的宣告類型為**AdVarChar** ，而**DefinedSize**屬性值為50，其中包含單一字元。 它所傳回的**ActualSize**屬性值是單一字元的長度（以位元組為單位）。  
  
### <a name="determining-field-contents"></a>判斷欄位內容  
 資料來源中的資料行識別碼是以**欄位**的**名稱**屬性來表示。 **Field**物件的**Value**屬性會傳回或設定欄位的實際資料內容。 這是預設屬性。  
  
 若要變更欄位中的資料，請將**value**屬性設定為等於正確類型的新值。 您的資料指標類型必須支援更新以變更欄位的內容。 在此情況下，不會在批次模式中執行資料庫驗證，因此當您在這種情況下呼叫**UpdateBatch**時，您必須檢查是否有錯誤。 某些提供者也支援 ADO **Field**物件的**UnderlyingValue**和**OriginalValue**屬性，可在您嘗試執行批次更新時，協助您解決衝突。 如需如何解決這類衝突的詳細資訊，請參閱[編輯資料](../../../ado/guide/data/editing-data.md)。  
  
> [!NOTE]
>  將新**欄位**附加至**記錄集**時，無法設定**記錄集域**值。 相反地，新的**欄位**可以附加至已關閉的**記錄集**。 然後，必須開啟**記錄集**，然後才可以將值指派給這些**欄位**。  
  
### <a name="getting-more-field-information"></a>取得更多欄位資訊  
 ADO 物件有兩種屬性類型：內建和動態。 到目前為止，只討論**Field**物件的內建屬性。  
  
 內建屬性是在 ADO 中實和使用`MyObject.Property`語法立即提供給任何新物件的屬性。 它們不會在物件的**Properties**集合中顯示為**屬性**物件。  
  
 動態屬性是由基礎資料提供者所定義，而且會出現在適當 ADO 物件的**properties**集合中。 例如，提供者特定的屬性可能會指出**記錄集**物件是否支援交易或更新。 這些額外的屬性會以**屬性**物件的形式顯示在該**記錄集**物件的**properties**集合中。 只能透過集合使用語法`MyObject.Properties(0)`或`MyObject.Properties("Name")`來參考動態屬性。  
  
 您不能刪除任何一種屬性。  
  
 動態**屬性**物件有四個本身的內建屬性：  
  
-   **Name**屬性是可識別屬性的字串。  
  
-   **Type**屬性是指定屬性資料類型的整數。  
  
-   **Value**屬性是包含屬性設定的 variant。 **Value**是**屬性**物件的預設屬性。  
  
-   **Attributes**屬性是**Long**值，指出提供者特定屬性的特性。  
  
 **Field**物件的**Properties**集合包含欄位的其他相關中繼資料。 此集合的內容會根據提供者而有所不同。 下列程式碼範例會檢查本節開頭所引進之範例**記錄集**的**Properties**集合。 它會先查看集合的內容。 此程式碼會使用[SQL Server 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，因此**Properties**集合會包含該提供者的相關資訊。  
  
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
 在**欄位**物件上使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法，以完整的二進位或字元資料來填滿它。 在系統記憶體有限的情況下，您可以使用**AppendChunk**方法來管理部分中的長值，而不是完整的。  
  
 如果**欄位**物件的**Attributes**屬性中的**adFldLong**位設定為**True**，您可以針對該欄位使用**AppendChunk**方法。  
  
 **Field**物件上的第一個**AppendChunk**呼叫會將資料寫入欄位，並覆寫任何現有的資料。 後續的**AppendChunk**呼叫會新增至現有的資料。 如果您要將資料附加至一個欄位，然後設定或讀取目前記錄中另一個欄位的值，ADO 會假設您已完成將資料附加至第一個欄位。 如果您再次呼叫第一個欄位上的**AppendChunk**方法，ADO 會將呼叫解讀為新的**AppendChunk**作業，並覆寫現有的資料。 存取不是第一個**記錄集**物件複製之其他**記錄集**物件中的欄位，將不會中斷**AppendChunk**作業。  
  
 請在**Field**物件上使用**GetChunk**方法，以取出部分或整個完整的二進位或字元資料。 在系統記憶體受到限制的情況下，您可以使用**GetChunk**方法來管理部分中的長數值，而不是完整的值。  
  
 **GetChunk**呼叫傳回的資料會指派給*變數*。 如果*大小*大於剩餘的資料， **GetChunk**方法只會傳回剩餘的資料，而不含空格的填補*變數*。 如果欄位是空的，則**GetChunk**方法會傳回 null 值。  
  
 每個後續的**GetChunk**呼叫都會從先前的**GetChunk**呼叫停止的位置，抓取開始的資料。 不過，如果您要從某個欄位抓取資料，然後設定或讀取目前記錄中另一個欄位的值，ADO 會假設您已完成從第一個欄位抓取資料。 如果您再次呼叫第一個欄位上的**GetChunk**方法，ADO 會將呼叫解讀為新的**GetChunk**作業，並開始讀取資料的開頭。 存取不是第一個**記錄集**物件複製之其他**記錄集**物件中的欄位，將不會中斷**GetChunk**作業。  
  
 如果**欄位**物件的**Attributes**屬性中的**adFldLong**位設定為**True**，您可以針對該欄位使用**GetChunk**方法。  
  
 當您在**欄位**物件上使用**GetChunk**或**AppendChunk**方法時，如果沒有目前的記錄，則會發生錯誤3021（沒有目前的記錄）。  
  
 如需使用這些方法來操作二進位資料的範例，請參閱 ADO 程式設計*人員參考*中的[AppendChunk 方法](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk 方法](../../../ado/reference/ado-api/getchunk-method-ado.md)範例。
