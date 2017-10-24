---
title: "提示屬性動態 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 065656ea3023b1526573a48cd6d7d21eee6f6179
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="prompt-property-dynamic-ado"></a>提示屬性動態 (ADO)
指定的 OLE DB 提供者是否應提示使用者輸入的初始化資訊。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定並傳回[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)值。  
  
## <a name="remarks"></a>備註  
 **提示**是動態屬性，可能會附加至[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)OLE DB 提供者的集合。 若要初始化資訊的提示，OLE DB 提供者通常會顯示對話方塊給使用者。  
  
 動態屬性[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件時，遺失了**連接**已關閉。 **提示**必須重設屬性，然後再重新開啟**連接**使用預設值以外的值。  
  
> [!NOTE]
>  請勿指定提供者應該會提示使用者在案例中的使用者將無法回應 對話方塊中。 比方說，使用者將無法在使用者的用戶端，而不是伺服器系統上執行應用程式，或是在系統上沒有使用者登入以執行應用程式回覆。 在這些情況下，應用程式將會無限期地等候回應，並看上去可以鎖定。  
  
## <a name="usage"></a>使用方式  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>適用於  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

