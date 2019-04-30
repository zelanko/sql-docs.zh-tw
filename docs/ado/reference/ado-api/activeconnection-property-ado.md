---
title: ActiveConnection 屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 951f43a2842162aa00f664dc83b754d06d8aafb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065536"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 屬性 (ADO)
表示要[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件指定[命令](../../../ado/reference/ado-api/command-object-ado.md)，[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，或[記錄](../../../ado/reference/ado-api/record-object-ado.md)目前所屬的物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，其中包含連線的定義，如果連線已關閉，或是**Variant**包含目前**連接**物件連接已開啟。 預設值為 null 物件參考。 請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性。  
  
## <a name="remarks"></a>備註  
 使用**ActiveConnection**屬性，以判斷**連線**物件的指定**命令**將會執行物件或指定**資料錄集**隨即開啟。  
  
## <a name="command"></a>命令  
 針對**命令**物件， **ActiveConnection**屬性是讀取/寫入。  
  
 如果您嘗試呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法**命令**之前將此屬性設定為 開啟物件**連接**物件或有效的連接字串，就會發生錯誤。  
  
 如果**連接**物件指派給**ActiveConnection**屬性，必須開啟的物件。 指派已關閉的連接物件會造成錯誤。  
  
### <a name="note"></a>附註  
 **Microsoft Visual Basic**設定**ActiveConnection**屬性設*Nothing*解除**命令**物件從目前**連接**並造成提供者發行資料來源上的任何相關聯的資源。 您可以將產生關聯**命令**具有相同或另一個物件**連線**物件。 某些提供者可讓您變更屬性設定從某個**連接**到另一個，而不必先將屬性設定為*Nothing*。  
  
 如果[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)的集合**命令**物件包含的提供者所提供的參數，如果您將會清除集合**ActiveConnection**屬性，以*Nothing*或另一個**連線**物件。 如果您以手動方式建立[參數](../../../ado/reference/ado-api/parameter-object.md)物件，並使用它們來填滿**參數**集合**命令**物件，設定**ActiveConnection**屬性，以*Nothing*或另一個**連線**物件分葉**參數**保持不變的集合。  
  
 關閉**連接**可用物件**命令**物件是相關聯的集**ActiveConnection**屬性設*Nothing*。 將這個屬性設定為已關閉**連線**物件會產生錯誤。  
  
## <a name="recordset"></a>資料錄集  
 開啟**Recordset**物件或**資料錄集**物件，而其[來源](../../../ado/reference/ado-api/source-property-ado-recordset.md)屬性設定為有效**命令**物件，而**ActiveConnection**屬性是唯讀的。 否則，它是讀取/寫入。  
  
 您可以將此屬性設定為有效**連線**物件或有效的連接字串。 在此情況下，提供者會建立新**連線**物件使用這個定義，並開啟連接。 此外，提供者可能會將此屬性設定新**連接**可讓您存取的物件**連線**物件取得擴充的錯誤資訊，或執行其他命令。  
  
 如果您使用*ActiveConnection*引數[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來開啟**資料錄集**物件**ActiveConnection**屬性繼承的引數的值。  
  
 如果您設定**來源**屬性**資料錄集**設為有效的物件**命令**物件變數**ActiveConnection**屬性**Recordset**繼承的設定**命令**物件的**ActiveConnection**屬性。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端上使用時**資料錄集**物件，可以設定這個屬性，只對連接字串，或 （在 Microsoft Visual Basic 或 Visual Basic Scripting Edition） *Nothing*.  
  
## <a name="record"></a>記錄  
 這個屬性是讀取/寫入時**記錄**物件會關閉，而可能包含連接字串或參考開放式**連線**物件。 這個屬性是唯讀的時機**記錄**物件已開啟，並包含開啟的參考**連線**物件。  
  
 A**連接**物件會隱含地建立當**記錄**從 URL 開啟物件。 開啟**記錄**的現有開啟**連線**藉由指定的物件**連接**物件給這個屬性，或使用**連接**物件做為參數，在[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法呼叫。 如果**記錄**開啟從現有**記錄**或[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，然後它會自動關聯於可**記錄**或**資料錄集**物件的**連線**物件。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
