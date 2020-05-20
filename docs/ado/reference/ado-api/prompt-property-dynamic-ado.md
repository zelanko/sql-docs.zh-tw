---
title: Prompt 屬性-動態（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e99273a94fc38779b50203d3dd5b78106f6a90c6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761916"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 動態屬性 (ADO)
指定 OLE DB 提供者是否應該提示使用者提供初始化資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)值。  
  
## <a name="remarks"></a>備註  
 [**提示**] 是動態屬性，可由 OLE DB 提供者附加至[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。 若要提示輸入初始化資訊，OLE DB 提供者通常會向使用者顯示對話方塊。  
  
 **連接關閉**時，[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的動態屬性會遺失。 在重新開啟**連接**之前，必須先重設**Prompt**屬性，才能使用預設值以外的值。  
  
> [!NOTE]
>  請勿指定提供者應該在使用者將無法回應對話方塊的情況下，提示使用者。 例如，如果應用程式是在伺服器系統上執行，而不是在使用者的用戶端上執行，或如果應用程式是在沒有使用者登入的系統上執行，使用者將無法回應。 在這些情況下，應用程式會無限期地等待回應，而且似乎會鎖定。  
  
## <a name="usage"></a>使用量  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
