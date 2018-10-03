---
title: 提供者屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22ee1b88ee6065a49c53ae7024c93e869099ca3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755286"
---
# <a name="provider-property-ado"></a>Provider 屬性 (ADO)
指出提供者的名稱[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，指出提供者名稱。  
  
## <a name="remarks"></a>備註  
 使用**提供者**屬性來設定或傳回連接的提供者的名稱。 這個屬性也可以設定的內容所[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性或*ConnectionString*引數[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法; 不過，指定提供者同時呼叫的多個就地**開啟**方法可能會有無法預期的結果。 如果未不指定任何提供者，則屬性會預設為 MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md))。  
  
 **提供者**屬性是讀取/寫入，當連接已關閉，且為唯讀狀態開啟時。 此設定才會生效直到您請開啟**連接**物件或存取[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合**連接**物件。 如果設定不是有效的就會發生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Provider 和 DefaultDatabase 屬性範例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 屬性範例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md)
