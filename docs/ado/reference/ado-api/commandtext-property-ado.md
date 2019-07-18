---
title: CommandText 屬性 (ADO) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919721"
---
# <a name="commandtext-property-ado"></a>CommandText 屬性 (ADO)
表示要對提供者發出的命令文字。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 取得或設定**字串**值，其中包含提供者命令，例如 SQL 陳述式、 資料表名稱、 相對的 URL 或預存程序呼叫。 預設值為空字串 ("")。  
  
## <a name="remarks"></a>備註  
 使用**CommandText**屬性來設定或傳回由命令文字[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 通常，這會是 SQL 陳述式，但也可以是任何其他類型的提供者，例如預存程序呼叫所辨識的命令陳述式。 SQL 陳述式必須是特定方言或提供者的查詢處理器所支援的版本。  
  
 如果[已準備](../../../ado/reference/ado-api/prepared-property-ado.md)屬性**命令**物件設定為**True**而**命令**物件繫結至開啟的連接設定時**CommandText** ADO 準備查詢 （也就是提供者所儲存的查詢的編譯形式） 的屬性，當您呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)或[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法。  
  
 取決於[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)可能會改變屬性設定，ADO **CommandText**屬性。 您可以閱讀**CommandText**在任何時間，以查看實際的命令文字的屬性在執行期間，會使用該 ADO。  
  
 使用**CommandText**屬性來設定或傳回指定的資源，例如檔案或目錄的相對 URL。 資源是絕對 URL，或隱含地開啟明確指定位置的相對[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向屬性範例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
