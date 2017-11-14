---
title: "提供者屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1839d8bc9c954d3f5ceeafca2b604304801f643f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="provider-property-ado"></a>提供者屬性 (ADO)
指出提供者的名稱[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，指出提供者名稱。  
  
## <a name="remarks"></a>備註  
 使用**提供者**屬性來設定或傳回連接的提供者的名稱。 這個屬性也可以設定的內容[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性或*ConnectionString*引數的[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法; 不過，指定提供者在多個位置呼叫**開啟**方法可能都有無法預期的結果。 如果未不指定任何提供者，則屬性會預設為 MSDASQL ([Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md))。  
  
 **提供者**屬性是讀取/寫入，當連接已關閉，且為唯讀模式開啟時。 設定不會影響直到您開啟**連接**物件或存取[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合**連接**物件。 如果設定不是有效的就會發生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [提供者和 DefaultDatabase 屬性範例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [提供者和 DefaultDatabase 屬性範例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [附錄 a： 提供者](../../../ado/guide/appendixes/appendix-a-providers.md)

