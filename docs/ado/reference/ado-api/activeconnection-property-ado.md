---
description: ActiveConnection 屬性 (ADO)
title: " (ADO) 的 ActiveConnection 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bc1a54d70639e4e3ff78748b4e04483fcfefafdb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976959"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 屬性 (ADO)
指出指定的[命令](./command-object-ado.md)、[記錄集](./recordset-object-ado.md)或[記錄](./record-object-ado.md)物件目前所屬的[連接](./connection-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 如果連接已關閉，則設定或傳回包含連接定義的**字串**值，如果連接已開啟，則為包含目前**連接**物件的**變數**。 預設值為 null 物件參考。 請參閱 [ConnectionString](./connectionstring-property-ado.md) 屬性。  
  
## <a name="remarks"></a>備註  
 您可以使用**ActiveConnection**屬性來判斷指定的**命令**物件將執行的**連接**物件，或是將開啟指定的**記錄集**。  
  
## <a name="command"></a>Command  
 針對 **命令** 物件， **ActiveConnection** 屬性為 read/write。  
  
 如果您嘗試在**命令**物件上呼叫[Execute](./execute-method-ado-command.md)方法，然後將這個屬性設定為開啟的**連接**物件或有效的連接字串，就會發生錯誤。  
  
 如果 **連接** 物件已指派給 **ActiveConnection** 屬性，則必須開啟物件。 指派封閉的連線物件會導致錯誤。  
  
### <a name="note"></a>注意  
 **Microsoft Visual Basic** 將 **ActiveConnection** 屬性設定為 *Nothing* ，就不會將 **命令** 物件與目前的 **連接** 解除關聯，而會導致提供者釋出資料來源上任何相關聯的資源。 然後，您可以將 **命令** 物件與相同或其他 **連接** 物件產生關聯。 有些提供者可讓您將屬性設定從一個 **連接** 變更為另一個連接，而不需要先將屬性設定為 *Nothing*。  
  
 如果**Command**物件的[parameters](./parameters-collection-ado.md)集合包含提供者所提供的參數，則如果您將**ActiveConnection**屬性設定為*Nothing*或另一個**連接**物件，則會清除集合。 如果您手動建立[參數](./parameter-object.md)物件，並使用它們來填滿**Command**物件的**Parameters**集合，則將**ActiveConnection**屬性設定為*Nothing*或另一個**連接**物件會讓**參數**集合保持不變。  
  
 關閉與**Command**物件相關聯的**連接**物件，會將**ActiveConnection**屬性設定為*Nothing*。 將這個屬性設定為已關閉的 **連接** 物件會產生錯誤。  
  
## <a name="recordset"></a>資料錄集  
 針對開啟的**記錄集**物件，或針對[其 Source](./source-property-ado-recordset.md)屬性設為有效**命令**物件的**記錄集**物件， **ActiveConnection**屬性為唯讀。 否則，它會是讀取/寫入。  
  
 您可以將此屬性設定為有效的 **連接** 物件或有效的連接字串。 在此情況下，提供者會使用此定義來建立新的 **連接** 物件，並開啟連接。 此外，提供者可能會將這個屬性設定為新的 **連接** 物件，讓您能夠存取 **連接** 物件以取得擴充的錯誤資訊或執行其他命令。  
  
 如果您使用[open](./open-method-ado-recordset.md)方法的*ActiveConnection*引數來開啟**記錄集**物件， **ActiveConnection**屬性將會繼承引數的值。  
  
 如果您將**記錄集**物件的 [**來源**] 屬性設定為有效的**命令**物件變數，**記錄集**的**ActiveConnection**屬性就會繼承**命令**物件之**ActiveConnection**屬性的設定。  
  
> [!NOTE]
>  **遠端資料服務使用量** 在用戶端 **記錄集** 物件上使用時，此屬性只能設定為連接字串或 (在 Microsoft Visual Basic 或 Visual Basic 中，腳本版本) 為 *Nothing*。  
  
## <a name="record"></a>Record  
 當 **記錄** 物件關閉時，這個屬性是讀取/寫入，而且可能包含連接字串或開啟 **連接** 物件的參考。 當 **記錄** 物件開啟時，這個屬性是唯讀的，而且包含開啟之 **連接** 物件的參考。  
  
 從 URL 開啟**記錄**物件時，會隱含地建立**連接**物件。 藉由將**連接**物件指派給這個屬性，或在[open](./open-method-ado-record.md)方法呼叫中使用**connection**物件做為參數，以現有的開啟**連接**物件開啟**記錄**。 如果從現有的**記錄**或[記錄集](./recordset-object-ado.md)開啟**記錄**，則會自動**與該記錄**或記錄**集**物件的連線物件**建立**關聯。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Command 物件 (ADO)](./command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record 物件 (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VB) ](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (VC + +) ](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例 (JScript) ](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ (ADO) 的 Connection 物件 ](./connection-object-ado.md)   
 [ConnectionString 屬性 (ADO)](./connectionstring-property-ado.md)