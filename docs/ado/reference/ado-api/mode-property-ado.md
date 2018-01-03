---
title: "模式屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords: Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21a3257ff92cd73d10f0685a7727d98417a917ef
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="mode-property-ado"></a>模式屬性 (ADO)
表示可用的權限中修改資料[連接](../../../ado/reference/ado-api/connection-object-ado.md)，[記錄](../../../ado/reference/ado-api/record-object-ado.md)，或[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值。 預設值為**連接**是**adModeUnknown**。 預設值為**記錄**物件是**adModeRead**。 預設值為**資料流**基礎來源相關聯 (使用 URL 做為來源，或做為預設開啟**資料流**的**記錄**) 是**adModeRead**。 預設值為**資料流**不相關聯的基礎來源 （在記憶體中具現化） 是**adModeUnknown**。  
  
## <a name="remarks"></a>備註  
 使用**模式**屬性來設定，或在目前的連線提供者所傳回的存取權限使用中。 您可以設定**模式**屬性時，才**連接**物件已關閉。  
  
 如**資料流**物件，如果未指定存取模式，它繼承自來源用來開啟**資料流**物件。 例如，如果**資料流**開啟從**記錄**物件，依預設開啟相同的模式為**記錄**。  
  
 當物件已關閉，且為唯讀狀態開啟物件時，這個屬性是讀取/寫入。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用用戶端時**連接**物件**模式**屬性只能設定為**adModeUnknown**。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>請參閱  
 [IsolationLevel 和模式屬性範例 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和模式屬性範例 （VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
