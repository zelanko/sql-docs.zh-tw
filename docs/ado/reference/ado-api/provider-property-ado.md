---
description: Provider 屬性 (ADO)
title: " (ADO) 的提供者屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c3f45e8652568bd0440121e27ee6ee0c116e676
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989909"
---
# <a name="provider-property-ado"></a>Provider 屬性 (ADO)
表示 [連接](./connection-object-ado.md) 物件的提供者名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回表示提供者名稱的 **字串** 值。  
  
## <a name="remarks"></a>備註  
 使用 **provider** 屬性來設定或傳回連接之提供者的名稱。 這個屬性也可以由[ConnectionString](./connectionstring-property-ado.md)屬性的內容或[Open](./open-method-ado-connection.md)方法的*connectionstring*引數來設定;不過，在呼叫**Open**方法時，在一個以上的位置指定提供者可能會產生無法預期的結果。 如果未指定提供者，屬性將預設為 MSDASQL ([Microsoft OLE DB provider FOR ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)) 。  
  
 當連線關閉時， **提供者** 屬性是讀取/寫入，而當連接開啟時，則是唯讀的。 除非您開啟**連接**物件或存取**連接**物件的[屬性](./properties-collection-ado.md)集合，否則設定不會生效。 如果設定無效，則會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Provider 和 DefaultDatabase 屬性範例 (VB) ](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 屬性範例 (VB) ](./provider-and-defaultdatabase-properties-example-vb.md)   
 [Microsoft OLE DB Provider for ODBC](../../guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [附錄 A：提供者](../../guide/appendixes/appendix-a-providers.md)