---
title: Prompt 動態屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cde7a5ad0324bc7d5cde5e1a794eeb9e2cb3381a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931586"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 動態屬性 (ADO)
指定的 OLE DB 提供者是否應該提示使用者提供初始化資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定，並傳回[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)值。  
  
## <a name="remarks"></a>備註  
 **提示**是動態屬性，可以附加[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)OLE DB 提供者的集合。 若要提示初始化資訊，OLE DB 提供者通常會顯示一個對話方塊給使用者。  
  
 動態屬性[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件時，遺失了**連線**已關閉。 **提示**必須重設屬性，然後再重新開啟**連線**使用預設值以外的值。  
  
> [!NOTE]
>  未指定提供者應該會提示使用者在所在的使用者將無法回應 對話方塊中的案例中。 例如，使用者將無法回應，如果使用者的用戶端，而不是伺服器系統上執行應用程式，或在系統上執行應用程式使用沒有使用者登入。 在這些情況下，將會無限期地等待回應的應用程式，並將其似乎鎖定中。  
  
## <a name="usage"></a>使用量  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
