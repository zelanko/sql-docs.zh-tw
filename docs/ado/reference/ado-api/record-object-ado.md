---
description: Record 物件 (ADO)
title: " (ADO) 的記錄物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: rothja
ms.author: jroth
ms.openlocfilehash: 6860e10d3639fcbfdf59e8ff5fe8a5a8b675662a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772597"
---
# <a name="record-object-ado"></a>Record 物件 (ADO)
表示來自 [記錄集](./recordset-object-ado.md) 或資料提供者的資料列，或是由半結構化資料提供者（例如檔案或目錄）所傳回的物件。  
  
## <a name="remarks"></a>備註  
 **記錄**物件代表一個資料列，而且與一個資料列**記錄集**有一些概念相似之處。 視您提供者的功能而定， **記錄** 物件可能會直接從您的提供者傳回，而不是單一資料列 **記錄集**，例如，當只選取一個資料列的 SQL 查詢執行時。 或者，您可以直接從**記錄集**物件取得**記錄**物件。 或者，您可以直接從提供者將 **記錄** 傳回至半結構化資料，例如 Microsoft Exchange OLE DB 提供者。  
  
 您可以透過**記錄**物件上的[fields](./fields-collection-ado.md)集合，來查看與**記錄**物件相關聯的欄位。 ADO 允許在**記錄**物件的**Fields**集合中包含**記錄集**、 **SafeArray**和純量值在內的物件值資料行。  
  
 如果**記錄**物件代表**記錄集**內的資料列，則可以使用[Source](./source-property-ado-record.md)屬性返回該原始**記錄集**。  
  
 **記錄**物件也可以由半結構化資料提供者（例如， [Microsoft OLE DB Provider for Internet 發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)）用於模型樹狀結構命名空間。 樹狀結構中的每個節點都是具有相關聯資料行的 **記錄** 物件。 這些資料行可以代表該節點的屬性和其他相關資訊。 **記錄**物件可以同時代表樹狀結構中的分葉節點和非分葉節點。 非分葉節點的內容有其他節點，但分葉節點沒有這類內容。 分葉節點通常包含資料的二進位資料流程，而非分葉節點也可能有與其相關聯的預設二進位資料流程。 **Record**物件上的屬性會識別節點的型別。  
  
 **記錄**物件也代表流覽階層式組織資料的替代方式。 您可以建立 **記錄** 物件來代表大型樹狀結構中特定子樹狀結構的根，並且可以開啟新的 **記錄** 物件來代表子節點。  
  
 資源 (例如，檔案或目錄) 可以用絕對 URL 來唯一識別。 當使用絕對 URL 開啟**記錄**時，會隱含地建立[連接](./connection-object-ado.md)物件，並將其設定為**記錄**物件。 **連接**物件可以透過[ActiveConnection](./activeconnection-property-ado.md)屬性明確設定為**Record**物件。 使用**Connection**物件可以存取的檔案和目錄會定義**記錄**作業可能發生的*內容*。  
  
 **記錄**物件上的資料修改和導覽方法也會接受相對 url，此 url 會使用絕對 Url 或**連接**物件內容作為起點來尋找資源。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
 **連接**物件與每個**記錄**物件相關聯。 因此， **記錄** 物件作業可以藉由叫用 **連接** 物件交易方法來成為交易的一部分。  
  
 **記錄**物件不支援 ADO 事件，因此不會回應通知。  
  
 使用 **記錄** 物件的方法和屬性，您可以執行下列動作：  
  
-   使用[ActiveConnection](./activeconnection-property-ado.md)屬性設定或傳回相關聯的**連接**物件。  
  
-   使用 [Mode](./mode-property-ado.md) 屬性工作表示存取權限。  
  
-   傳回目錄的 URL （如果有的話），其中包含具有[ParentURL](./parenturl-property-ado.md)屬性之**記錄**所表示的資源。  
  
-   指出使用[來源](./source-property-ado-record.md)屬性衍生**記錄**的絕對 url、相對 url 或**記錄集**。  
  
-   以[State](./state-property-ado.md)屬性工作表示**記錄**的目前狀態。  
  
-   **Record**  -  使用[RecordType](./recordtype-property-ado.md)屬性，表示記錄的*簡單*、*集合*或*結構化檔*的類型。  
  
-   使用 [Cancel](./cancel-method-ado.md) 方法停止執行非同步作業。  
  
-   將資料來源中的 **記錄** 與 [Close](./close-method-ado.md) 方法解除關聯。  
  
-   使用[CopyRecord](./copyrecord-method-ado.md)方法，將**記錄**所表示的檔案或目錄複寫到另一個位置。  
  
-   使用[DeleteRecord](./deleterecord-method-ado.md)方法刪除**記錄**所表示的檔案（或目錄和子目錄）。  
  
-   開啟包含資料列的**記錄集**，這些資料列會以[GetChildren](./getchildren-method-ado.md)方法來表示**記錄**所代表之實體的子目錄和檔案。  
  
-   使用[MoveRecord](./moverecord-method-ado.md)方法，將 (重新命名) 檔案或目錄和子目錄，以**記錄**呈現至另一個位置。  
  
-   將 **記錄** 與現有的資料來源建立關聯，或使用 [Open](./open-method-ado-record.md) 方法建立新的檔案或目錄。  
  
 **記錄**物件可以安全地進行腳本處理。  
  
 本節包含下列主題。  
  
-   [Record 物件屬性、方法和事件](./record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的欄位集合 ](./fields-collection-ado.md)   
 [ (ADO) 的屬性集合 ](./properties-collection-ado.md)   
 [記錄和資料流程](../../guide/data/records-and-streams.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)