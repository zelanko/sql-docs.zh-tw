---
title: ActiveConnection 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dabf974e36b1f6beaff36f3a4888c128d7dfe1b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921517"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 屬性 (ADO)
指出指定的[命令](../../../ado/reference/ado-api/command-object-ado.md)、[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)或[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件目前所屬的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 如果連接已關閉，則設定或傳回包含連接定義的**字串**值; 如果連接已開啟，則為包含目前**連接**物件的**Variant** 。 預設值為 null 物件參考。 請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性。  
  
## <a name="remarks"></a>備註  
 使用**ActiveConnection**屬性來判斷指定的**命令**物件將會執行的**連接**物件，或指定的**記錄集**將會開啟。  
  
## <a name="command"></a>Command  
 對於**命令**物件， **ActiveConnection**屬性是可讀寫的。  
  
 如果您嘗試在**命令**物件上呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法，再將此屬性設定為開啟的**連接**物件或有效的連接字串，則會發生錯誤。  
  
 如果**連接**物件已指派給**ActiveConnection**屬性，則必須開啟物件。 指派關閉的連線物件會造成錯誤。  
  
### <a name="note"></a>注意  
 **Microsoft Visual Basic**將 [ **ActiveConnection** ] 屬性設定為 [*無*] 會解除目前**連接**的**命令**物件，並使提供者釋放資料來源上的任何相關聯資源。 然後，您可以將**命令**物件與相同或其他**連接**物件產生關聯。 有些提供者可讓您將屬性設定從一個**連接**變更為另一個連線，而不需要先將屬性設定為 [*無*]。  
  
 如果**Command**物件的[parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合包含提供者所提供的參數，則如果您將**ActiveConnection**屬性設定為 [*無*] 或 [其他**連接**物件]，則會清除該集合。 如果您手動建立[參數](../../../ado/reference/ado-api/parameter-object.md)物件，並使用它們來填入**Command**物件的**Parameters**集合，則將**ActiveConnection**屬性設定為 [*無*] 或 [其他**連接**物件] 會讓**參數**收集保持不變。  
  
 關閉與**命令**物件相關聯的**連接**物件，會將**ActiveConnection**屬性設定為 [*無*]。 將此屬性設定為已關閉的**連接**物件會產生錯誤。  
  
## <a name="recordset"></a>資料錄集  
 若為開啟的**記錄集**物件或其[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性設定為有效**Command**物件的**記錄集**物件， **ActiveConnection**屬性會是唯讀的。 否則，它會是讀取/寫入。  
  
 您可以將此屬性設定為有效的**連接**物件或有效的連接字串。 在此情況下，提供者會使用此定義來建立新的**連接**物件，並開啟連接。 此外，提供者可能會將此屬性設定為新的**連接**物件，讓您能夠存取**連接**物件的延伸錯誤資訊或執行其他命令。  
  
 如果您使用[open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法的*ActiveConnection*引數來開啟**記錄集**物件，則**ActiveConnection**屬性會繼承引數的值。  
  
 如果您將**記錄集**物件的**Source**屬性設為有效的**Command**物件變數，則**記錄集**的**ActiveConnection**屬性就會繼承**Command**物件的**ActiveConnection**屬性設定。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**記錄集**物件上使用時，這個屬性只能設定為連接字串，或（在 Microsoft Visual Basic 或 Visual Basic，腳本版本）中的*任何*一個。  
  
## <a name="record"></a>Record  
 當**記錄**物件關閉時，這個屬性是讀取/寫入，而且可能包含連接字串或開啟**連接**物件的參考。 當**記錄**物件開啟時，這個屬性是唯讀的，而且包含開啟**連接**物件的參考。  
  
 從 URL 開啟**記錄**物件時，會隱含建立**連接**物件。 將**連接**物件指派給這個屬性，或使用**連接**物件做為[open](../../../ado/reference/ado-api/open-method-ado-record.md)方法呼叫中的參數，以開啟具有現有開放式**連接**物件的**記錄**。 如果**記錄**是從現有的**記錄**或[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)開啟，則它會自動與該**記錄**或**記錄集**物件的**連接**物件產生關聯。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VB）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（JScript）](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
