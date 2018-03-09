---
title: "記錄物件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa00ab893549eee36bc1d1b0e858c7bc326fb83b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="record-object-ado"></a>記錄物件 (ADO)
代表從一個資料列[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或資料提供者或傳回為半結構化的資料提供者，例如檔案或目錄的物件。  
  
## <a name="remarks"></a>備註  
 A**記錄**物件代表一個資料列的資料，而且有一個資料列的一些概念相似之處**資料錄集**。 視您的提供者的功能而定**記錄**可能傳回物件，直接從您的提供者，而不是一個資料列**資料錄集**時選取一個資料列的 SQL 查詢的範例為，執行。 或者，**記錄**物件可以直接從取得**資料錄集**物件。 或者，**記錄**可以直接從提供者傳回半結構化資料，例如 Microsoft Exchange OLE DB 提供者。  
  
 您可以檢視相關聯的欄位**記錄**物件透過[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合**記錄**物件。 ADO 可以讓物件值的資料行包括**資料錄集**， **SafeArray**，和純量值中的**欄位**集合**記錄**物件。  
  
 如果**記錄**物件中的資料列都代表**資料錄集**，便可傳回至該原始**資料錄集**與[來源](../../../ado/reference/ado-api/source-property-ado-record.md)屬性。  
  
 **記錄**物件也使用半結構化的資料提供者這類[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)、 建立模型樹狀結構的命名空間。 在樹狀目錄中的每個節點是**記錄**具有相關聯的資料行物件。 資料行可以表示的屬性，該節點以及其他相關資訊。 **記錄**物件可代表樹狀結構中的非分葉節點和分葉節點。 非分葉節點有其他節點，做為其內容，但分葉節點沒有這類內容。 分葉節點通常包含二進位資料流的和非分葉節點可能也有預設的二進位資料流，與它們相關聯。 屬性上的**記錄**物件識別節點的類型。  
  
 **記錄**物件也代表一種替代方式的巡覽以階層方式組織的資料。 A**記錄**物件可能會建立代表大型的樹狀結構中的特定子樹狀目錄的根目錄和新**記錄**物件可能已開啟來代表子節點。  
  
 由絕對 URL，可以唯一識別資源 （例如，檔案或目錄）。 A[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件隱含地建立並設定為**記錄**物件時**記錄**的絕對 URL。 A**連接**物件明確地設定為**記錄**物件透過[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。 檔案和目錄，可以使用來存取**連接**物件定義*內容*所在**記錄**作業可能會發生。  
  
 上的資料修改和瀏覽方法**記錄**物件也接受相對 URL，找出資源，使用絕對 URL 或**連接**物件內容，做為起點。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 A**連接**物件有關聯，與每個**記錄**物件。 因此，**記錄**物件作業可以是交易的一部分，藉由叫用**連接**交易方法的物件。  
  
 **記錄**物件不支援 ADO 事件，因此不會回應通知。  
  
 使用的方法和屬性的**記錄**物件，您可以執行下列：  
  
-   設定或傳回相關聯**連接**物件[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。  
  
-   表示與存取權限[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。  
  
-   如果有的話，包含表示的資源傳回目錄中，URL**記錄**與[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性。  
  
-   表示絕對 URL，相對 URL，或**資料錄集**從中**記錄**衍生與[來源](../../../ado/reference/ado-api/source-property-ado-record.md)屬性。  
  
-   指出目前的狀態**記錄**與[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性。  
  
-   表示型別**記錄**—*簡單*，*集合*，或*結構化文件*— 與[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)屬性。  
  
-   停止執行非同步作業與[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   取消關聯**記錄**從資料來源與[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   複製檔案或目錄所代表**記錄**有另一個位置[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)方法。  
  
-   刪除檔案或目錄和子目錄，由**記錄**與[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)方法。  
  
-   開啟**資料錄集**，其中包含代表的子目錄和檔案所代表之實體的資料列**記錄**與[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)方法。  
  
-   移動 （重新命名） 檔案或目錄和子目錄，由**記錄**有另一個位置[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)方法。  
  
-   關聯**記錄**與現有的資料來源，或建立新的檔案或目錄[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法。  
  
 **記錄**物件而言是安全的指令碼。  
  
 本章節包含下列主題。  
  
-   [Record 物件屬性、方法和事件](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [記錄和資料流](../../../ado/guide/data/records-and-streams.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
