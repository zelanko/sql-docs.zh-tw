---
description: Field 物件
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 16f1b85006366702b0f95d5a41a74abf91ac7997
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452760"
---
# <a name="the-field-object"></a>Field 物件
每個 **Field** 物件通常會對應至資料庫資料表中的資料行。 但是， **欄位** 也可以表示另一個 **記錄集**的指標，稱為「章節」。 本指南稍後將會討論例外，例如章節資料行。  
  
 您可以使用 [**欄位**物件] 的 [**值**] 屬性來設定或傳回目前記錄的資料。 視提供者公開的功能而定，可能無法使用 **欄位** 物件的某些集合、方法或屬性。  
  
 使用 **Field** 物件的集合、方法和屬性，您可以執行下列動作：  
  
-   使用 **name** 屬性傳回欄位的名稱。  
  
-   使用 **Value** 屬性來查看或變更欄位中的資料。 **Value** 是 **Field** 物件的預設屬性。  
  
-   使用 **Type**、 **Precision**和 **NumericScale** 屬性，傳回欄位的基本特性。  
  
-   使用 **DefinedSize** 屬性傳回欄位的宣告大小。  
  
-   使用 **ActualSize** 屬性，傳回指定欄位中資料的實際大小。  
  
-   使用 **Attributes** 屬性和 **Properties** 集合，判斷特定欄位所支援的功能類型。  
  
-   使用 **AppendChunk** 和 **GetChunk** 方法，操作包含長二進位或長字元資料的欄位值。  
  
 如果提供者支援批次更新，請使用 **OriginalValue** 和 **UnderlyingValue** 屬性來解決批次更新期間的域值不一致。  
  
## <a name="describing-a-field"></a>描述欄位  
 接下來的主題將討論 [field](../../../ado/reference/ado-api/field-object.md) 物件的屬性，該物件代表描述 **欄位** 物件本身的資訊，也就是與欄位相關的中繼資料。 這項資訊可以用來判斷有關 **記錄集**架構的許多資訊。 這些屬性包括 **類型**、 **DefinedSize** 和 **ActualSize**、 **名稱**和 **NumericScale** 和 **精確度**。  
  
### <a name="discovering-the-data-type"></a>探索資料類型  
 **Type**屬性工作表示欄位的資料類型。 ADO 所支援的資料型別列舉常數，如 Ado 程式設計*人員參考*中的[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)所述。  
  
 針對浮點數類型（例如 **adNumeric**），您可以取得詳細資訊。 **NumericScale**屬性會指出小數點右邊的位數將用來表示**欄位**的值。 **Precision**屬性會指定用來表示**欄位**值的最大位數。  
  
### <a name="determining-field-size"></a>判斷欄位大小  
 您可以使用 **DefinedSize** 屬性來判斷 **Field** 物件的資料容量。  
  
 您可以使用 **ActualSize** 屬性來傳回 **欄位** 物件值的實際長度。 針對所有欄位， **ActualSize** 屬性是唯讀的。 如果 ADO 無法判斷 **欄位** 物件值的長度， **ActualSize** 屬性會傳回 **adUnknown**。  
  
 **DefinedSize**和**ActualSize**屬性有不同的用途。 例如，假設有一個 **Field** 物件，其宣告的型別為 **AdVarChar** ，而 **DefinedSize** 屬性值為50，其中包含單一字元。 它所傳回的 **ActualSize** 屬性值是單一字元的長度（以位元組為單位）。  
  
### <a name="determining-field-contents"></a>判斷欄位內容  
 資料來源中的資料行識別碼是以**欄位**的**名稱**屬性工作表示。 **Field**物件的**Value**屬性會傳回或設定欄位的實際資料內容。 這是預設屬性。  
  
 若要變更欄位中的資料，請將 **value** 屬性設為等於正確型別的新值。 您的資料指標類型必須支援更新，才能變更欄位的內容。 在這種情況下，不會在批次模式中執行資料庫驗證，因此當您在這種情況下呼叫 **UpdateBatch** 時，將需要檢查是否有錯誤。 有些提供者也支援 ADO **Field** 物件的 **UnderlyingValue** 和 **OriginalValue** 屬性，以協助您在嘗試執行批次更新時解決衝突。 如需如何解決這類衝突的詳細資訊，請參閱 [編輯資料](../../../ado/guide/data/editing-data.md)。  
  
> [!NOTE]
>  將新**欄位**附加至**記錄集**時，無法設定**記錄集域**值。 相反地，您可以將新 **欄位** 附加至已關閉的 **記錄集**。 然後，您必須開啟 **記錄集** ，才能將值指派給這些 **欄位**。  
  
### <a name="getting-more-field-information"></a>取得更多欄位資訊  
 ADO 物件有兩種類型的屬性：內建和動態。 到目前為止，只有 **Field** 物件的內建屬性已討論過。  
  
 內建屬性是在 ADO 中執行的屬性，而且可以使用語法立即提供給任何新的物件使用 `MyObject.Property` 。 它們不會在物件的**屬性**集合中顯示為**屬性**物件。  
  
 動態屬性是由基礎資料提供者所定義，而且會出現在適當 ADO 物件的 **properties** 集合中。 例如，提供者特定的屬性可能會指出 **記錄集** 物件是否支援交易或更新。 這些額外的屬性會在該**記錄集**物件的**properties**集合中顯示為**屬性**物件。 只有透過使用語法或的集合，才能參考動態屬性 `MyObject.Properties(0)` `MyObject.Properties("Name")` 。  
  
 您無法刪除任一種類型的屬性。  
  
 動態 **屬性** 物件有四個內建的屬性：  
  
-   **Name**屬性是識別屬性的字串。  
  
-   **Type**屬性是指定屬性資料類型的整數。  
  
-   **Value**屬性是包含屬性設定的變數。 **Value** 是 **屬性** 物件的預設屬性。  
  
-   **屬性**（attribute）屬性（attribute）是**Long**值，指出提供者特定屬性的特性。  
  
 **Field**物件的**Properties**集合包含與欄位相關的其他中繼資料。 此集合的內容會根據提供者而有所不同。 下列程式碼範例會檢查本章節開頭所引進之範例**記錄集**的**屬性**集合。 它會先查看集合的內容。 此程式碼會使用 [OLE DB 提供者進行 SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，因此 **屬性** 集合包含與該提供者相關的資訊。  
  
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
 在**欄位**物件上使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)方法，以完整的二進位或字元資料來填滿資料。 在系統記憶體受限的情況下，您可以使用 **AppendChunk** 方法來管理部分（而非全部）中的 long 值。  
  
 如果**field**物件的**Attributes**屬性中的**adFldLong**位設為**True**，則您可以針對該欄位使用**AppendChunk**方法。  
  
 **Field**物件的第一個**AppendChunk**呼叫會將資料寫入欄位，以覆寫任何現有的資料。 後續的 **AppendChunk** 呼叫會新增至現有的資料。 如果您要將資料附加至某個欄位，然後設定或讀取目前記錄中另一個欄位的值，則 ADO 會假設您已完成將資料附加至第一個欄位。 如果您再次在第一個欄位上呼叫 **AppendChunk** 方法，則 ADO 會將呼叫解讀為新的 **AppendChunk** 作業，並覆寫現有的資料。 存取其他 **記錄集** 物件中非第一個 **記錄集** 物件的欄位，將不會中斷 **AppendChunk** 作業。  
  
 在**欄位**物件上使用**GetChunk**方法，以取出部分或所有的完整二進位或字元資料。 在系統記憶體受限的情況下，您可以使用 **GetChunk** 方法，在部分（而不是整個）中操作長值。  
  
 **GetChunk**呼叫傳回的資料會指派給*變數*。 如果 *大小* 大於剩餘的資料， **GetChunk** 方法只會傳回剩餘的資料，但不含空格的填補 *變數* 。 如果欄位是空的， **GetChunk** 方法會傳回 null 值。  
  
 每個後續的 **GetChunk** 呼叫都會從先前的 **GetChunk** 呼叫離開的位置開始抓取資料。 但是，如果您要從某個欄位取出資料，然後設定或讀取目前記錄中另一個欄位的值，則 ADO 會假設您已完成從第一個欄位中取出資料。 如果您再次在第一個欄位上呼叫 **GetChunk** 方法，則 ADO 會將呼叫解讀為新的 **GetChunk** 作業，並開始從資料的開頭開始讀取。 存取其他 **記錄集** 物件中非第一個 **記錄集** 物件的欄位，將不會中斷 **GetChunk** 作業。  
  
 如果**field**物件的**Attributes**屬性中的**adFldLong**位設為**True**，則您可以針對該欄位使用**GetChunk**方法。  
  
 如果您在**欄位**物件上使用**GetChunk**或**AppendChunk**方法時沒有目前的記錄，則會發生錯誤 3021 (不會) 發生目前的記錄。  
  
 如需使用這些方法來操作二進位資料的範例，請參閱 ADO 程式設計*人員參考*中的[AppendChunk 方法](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk 方法](../../../ado/reference/ado-api/getchunk-method-ado.md)範例。
