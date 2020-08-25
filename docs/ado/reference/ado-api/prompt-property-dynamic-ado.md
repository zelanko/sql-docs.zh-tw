---
description: Prompt 動態屬性 (ADO)
title: Prompt 屬性-Dynamic (ADO) |Microsoft Docs
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
ms.openlocfilehash: 3f5e8d379f1ef2a756505675b2969374ec130feb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773017"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 動態屬性 (ADO)
指定 OLE DB 提供者是否應該提示使用者提供初始化資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回 [ConnectPromptEnum](./connectpromptenum.md) 值。  
  
## <a name="remarks"></a>備註  
 **Prompt** 是動態屬性，可由 OLE DB 提供者附加至 [連接](./connection-object-ado.md) 物件的 [屬性](./properties-collection-ado.md) 集合。 為了提示初始化資訊，OLE DB 提供者通常會對使用者顯示對話方塊。  
  
 **連接關閉**時，[連接](./connection-object-ado.md)物件的動態屬性會遺失。 **提示**屬性必須先重設，才能重新開啟**連接**，以使用預設值以外的值。  
  
> [!NOTE]
>  請勿指定提供者在使用者將無法回應對話方塊的情況下，提示使用者提示使用者。 例如，如果應用程式是在伺服器系統上執行，而不是在使用者的用戶端上執行，或應用程式是在沒有使用者登入的系統上執行，則使用者將無法回應。 在這些情況下，應用程式將會無限期地等候回應，而且似乎會鎖定。  
  
## <a name="usage"></a>使用方式  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](./connection-object-ado.md)