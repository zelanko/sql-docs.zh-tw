---
title: ParentURL 屬性 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00583d9a57d420797bd54a3535a5d27b364373df
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="parenturl-property-ado"></a>ParentURL 屬性 (ADO)
指出父系所指向的絕對 URL 字串[記錄](../../../ado/reference/ado-api/record-object-ado.md)的目前**記錄**物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**字串**值，指出父系的 URL**記錄**。  
  
## <a name="remarks"></a>備註  
 **ParentURL**屬性取決於用來開啟來源**記錄**物件。 例如，**記錄**可以使用包含相對路徑的目錄名稱所參考的來源開啟[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性。  
  
 假設 「 第二個"資料夾底下所含"first"。 開啟**記錄**物件可以使用下列語法：  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 現在，值`the` **ParentURL**屬性是`"http://first"`，與相同**ActiveConnection**。  
  
 來源也可以是絕對的 URL 這類`"http://first/second"`。 **ParentURL**屬性然後是`"http://first"`，上面的層級`"second"`。  
  
 如果這個屬性可能是 null 的值：  
  
-   沒有與目前物件的父系例如，如果**記錄**物件都代表目錄的根目錄。  
  
-   **記錄**物件都代表不能以 URL 指定的實體。  
  
 此屬性是唯讀的。  
  
> [!NOTE]
>  這個屬性才支援文件來源的提供者，例如[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[記錄和欄位 Provider-Supplied](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
> [!NOTE]
>  如果目前的記錄會包含從 ADO 資料錄**資料錄集**、 存取**ParentURL**屬性會導致執行階段錯誤，表示可能沒有 URL。  
  
## <a name="applies-to"></a>適用於  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
