---
title: Record 物件（ADO） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ffc515350bfff4307da382c05aae50ed1930802
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917364"
---
# <a name="record-object-ado"></a>Record 物件 (ADO)
表示來自[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或資料提供者的資料列，或由半結構化資料提供者（例如檔案或目錄）所傳回的物件。  
  
## <a name="remarks"></a>備註  
 **記錄**物件代表一個資料列，而且與單一資料列**記錄集**具有一些概念相似之處。 視提供者的功能而定，**記錄**物件可以直接從提供者傳回，而不是從一個資料列**記錄集**，例如，當執行只選取一個資料列的 SQL 查詢時。 或者，您可以直接從**記錄集**物件取得**記錄**物件。 或者，**記錄**可以直接從提供者傳回到半結構化資料，例如 Microsoft Exchange OLE DB 提供者。  
  
 您可以透過**record**物件上的[fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合，來查看與**記錄**物件相關聯的欄位。 ADO 允許物件值資料行，包括**記錄**物件的**Fields**集合中的**記錄集**、 **SafeArray**和純量值。  
  
 如果**記錄**物件代表**記錄集中**的資料列，則可以使用[Source](../../../ado/reference/ado-api/source-property-ado-record.md)屬性傳回給該原始**記錄集**。  
  
 **記錄**物件也可以由半結構化資料提供者（例如，用於[網際網路發行的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)）用於模型樹狀結構命名空間。 樹狀結構中的每個節點都是具有相關聯資料行的**記錄**物件。 這些資料行可以代表該節點的屬性和其他相關資訊。 **記錄**物件可以同時代表樹狀結構中的分葉節點和非分葉節點。 非分葉節點具有其他節點做為其內容，但分葉節點沒有這類內容。 分葉節點通常包含資料的二進位資料流程，而非分葉節點也可以有與其相關聯的預設二進位資料流程。 **記錄**物件上的屬性可識別節點的類型。  
  
 **Record**物件也代表流覽階層式組織資料的替代方式。 可能會建立**記錄**物件，以代表大型樹狀結構中特定子樹的根，而且可能會開啟新的**記錄**物件來代表子節點。  
  
 資源（例如，檔案或目錄）可由絕對 URL 來唯一識別。 當使用絕對 URL 開啟**記錄**時，會以隱含方式建立[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，並將它設定為**記錄**物件。 **連接**物件可以透過[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性明確地設定為**記錄**物件。 可以使用**Connection**物件存取的檔案和目錄會定義**記錄**作業可能發生的*內容*。  
  
 **記錄**物件上的資料修改和導覽方法也會接受相對 url，以使用絕對 Url 或**連接**物件內容做為起點來尋找資源。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **連接**物件與每個**記錄**物件相關聯。 因此，**記錄**物件作業可以藉由叫用**連接**物件交易方法，來成為交易的一部分。  
  
 **Record**物件不支援 ADO 事件，因此不會回應通知。  
  
 使用**Record**物件的方法和屬性，您可以執行下列動作：  
  
-   使用[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性來設定或傳回相關聯的**連接**物件。  
  
-   使用[Mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性來表示存取權限。  
  
-   傳回目錄的 URL （如果有的話），其中包含具有[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性的**記錄**所代表的資源。  
  
-   指出用[來源](../../../ado/reference/ado-api/source-property-ado-record.md)屬性衍生**記錄**的絕對 url、相對 URL 或**記錄集**。  
  
-   以[State](../../../ado/reference/ado-api/state-property-ado.md)屬性指出**記錄**的目前狀態。  
  
-   使用[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)屬性來表示**記錄** - 的類型，*簡單*、*集合*或*結構化檔*。  
  
-   使用[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)方法停止執行非同步作業。  
  
-   將資料來源中的**記錄**與[Close](../../../ado/reference/ado-api/close-method-ado.md)方法取消關聯。  
  
-   使用[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法，將**記錄**所代表的檔案或目錄複寫到另一個位置。  
  
-   使用[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)方法刪除**記錄**所表示的檔案或目錄和子目錄。  
  
-   開啟**記錄集**，其中包含的資料列代表使用[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)方法**記錄**所表示之實體的子目錄和檔案。  
  
-   使用[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法，將**記錄**所表示的檔案（或目錄和子目錄）移動（重新命名）到另一個位置。  
  
-   將**記錄**與現有的資料來源建立關聯，或使用[Open](../../../ado/reference/ado-api/open-method-ado-record.md)方法建立新的檔案或目錄。  
  
 **記錄**物件可安全地進行腳本處理。  
  
 本章節包含下列主題。  
  
-   [Record 物件屬性、方法和事件](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Fields 集合（ADO）](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [記錄和資料流程](../../../ado/guide/data/records-and-streams.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
