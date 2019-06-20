---
title: 記錄物件 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 859bf3f53051a500e86742cb681885b8067f6a0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712212"
---
# <a name="record-object-ado"></a>Record 物件 (ADO)
表示從資料列[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或資料提供者或為半結構化的資料提供者，例如檔案或目錄所傳回的物件。  
  
## <a name="remarks"></a>備註  
 A**記錄**物件代表一個資料列的資料，而且有一個資料列的某些概念相似之處**資料錄集**。 視您的提供者功能而定**記錄**可能會傳回物件，直接從您的提供者，而不是單一資料列**資料錄集**時選取 只有一個資料列的 SQL 查詢的範例為，執行。 或者，**記錄**可以取得物件，直接從**資料錄集**物件。 或者，**記錄**可以直接從提供者傳回給半結構化資料，例如 Microsoft Exchange OLE DB 提供者。  
  
 您可以檢視相關聯的欄位**記錄**物件透過[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)收集**記錄**物件。 ADO 可以讓物件值的資料行包括**資料錄集**， **SafeArray**，和純量值中的**欄位**集合**記錄**物件。  
  
 如果**記錄**物件表示中的資料列**資料錄集**，就可以返回至該原始**資料錄集**具有[來源](../../../ado/reference/ado-api/source-property-ado-record.md)屬性。  
  
 **記錄**物件也使用半結構化的資料提供者這類[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，來建立模型樹狀結構的命名空間。 在樹狀目錄中的每個節點**記錄**具有相關聯的資料行的物件。 資料行可以代表的屬性，該節點以及其他相關資訊。 **記錄**物件可以代表樹狀結構中的非分葉節點和分葉節點。 非分葉節點有其他節點，做為其內容，但分葉節點都沒有這類內容。 分葉節點通常包含二進位資料流和非分葉節點也有預設的二進位資料流，與其相關聯。 上的屬性**記錄**物件識別之節點的類型。  
  
 **記錄**物件也代表一種替代方式，針對瀏覽以階層方式組織資料。 A**記錄**物件可能是建立來代表大型樹狀結構中的特定子樹狀目錄的根目錄和新**記錄**物件可能會開啟至代表子節點。  
  
 由絕對 URL，可以唯一識別資源 （例如，檔案或目錄）。 A[連接](../../../ado/reference/ado-api/connection-object-ado.md)隱含地建立物件並設定為**記錄**物件時**記錄**開啟使用絕對 URL。 A**連接**物件可能明確地設定為**記錄**物件透過[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。 檔案和目錄，可以使用來存取**連接**物件定義*內容*所在**記錄**作業可能會發生。  
  
 上的資料修改和瀏覽方法**記錄**也接受物件的相對 URL，以找出資源，使用絕對 URL 或**連線**做為起點的物件內容。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 A**連接**物件會與每個關聯**記錄**物件。 因此，**記錄**物件的作業可以是交易的一部分，藉由叫用**連線**物件交易的方法。  
  
 **記錄**物件不支援 ADO 事件，因此不會回應通知。  
  
 使用的方法和屬性的**記錄**物件時，您可以執行下列動作：  
  
-   設定或傳回相關聯**連接**物件[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。  
  
-   指出使用的存取權限[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。  
  
-   傳回目錄的 URL，如果有的話，包含表示的資源**記錄**具有[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性。  
  
-   表示的絕對 URL 」、 「 相對 URL，或**Recordset**從中**記錄**衍生的[來源](../../../ado/reference/ado-api/source-property-ado-record.md)屬性。  
  
-   指出目前的狀態**記錄**具有[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性。  
  
-   表示型別**記錄** - *簡單*，*集合*，或*結構化文件*- [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)屬性。  
  
-   停止執行的非同步作業[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   取消關聯**記錄**與資料來源[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   複製檔案或所代表的目錄**記錄**到另一個位置，而[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
-   刪除檔案或目錄和子目錄，由**記錄**具有[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)方法。  
  
-   開啟**Recordset** ，其中包含代表的子目錄和檔案所代表之實體的資料列**記錄**具有[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)方法。  
  
-   移動 （重新命名） 的檔案或目錄和子目錄，由**記錄**到另一個位置，而[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
-   建立關聯**記錄**與現有的資料來源，或建立新的檔案或目錄[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法。  
  
 **記錄**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [Record 物件屬性、方法和事件](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [記錄和資料流](../../../ado/guide/data/records-and-streams.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
