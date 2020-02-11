---
title: CommandText 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0288dde74d2a172c9b0f8bdb865f4467fb0f637
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919721"
---
# <a name="commandtext-property-ado"></a>CommandText 屬性 (ADO)
表示要對提供者發出的命令文字。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 取得或設定**字串**值，其中包含提供者命令，例如 SQL 語句、資料表名稱、相對 URL 或預存程序呼叫。 預設值為空字串（""）。  
  
## <a name="remarks"></a>備註  
 使用**CommandText**屬性來設定或傳回[命令](../../../ado/reference/ado-api/command-object-ado.md)物件所代表之命令的文字。 這通常會是 SQL 語句，但也可以是提供者所識別的任何其他類型的命令語句，例如預存程序呼叫。 SQL 語句必須是提供者的查詢處理器所支援的特定方言或版本。  
  
 如果**命令**物件的[備](../../../ado/reference/ado-api/prepared-property-ado.md)妥屬性設定為**True** ，而且當您設定**CommandText**屬性時，**命令**物件會系結至開啟的連接，則當您呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)或[open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法時，ADO 會準備查詢（也就是提供者所儲存之查詢的已編譯形式）。  
  
 根據[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)屬性設定，ADO 可能會改變**CommandText**屬性。 您可以隨時讀取**CommandText**屬性，以查看 ADO 將在執行期間使用的實際命令文字。  
  
 使用**CommandText**屬性來設定或傳回指定資源（例如檔案或目錄）的相對 URL。 資源是相對於由絕對 URL 明確指定的位置，或是由開啟的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件所隱含的。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VB）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 屬性範例（JScript）](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
