---
title: ConnectModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: rothja
ms.author: jroth
ms.openlocfilehash: b9a25677f79ede93f8ea24e979d80dd13adff4fe
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242758"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
指定在[連接](../../../ado/reference/ado-api/connection-object-ado.md)中修改資料、開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)，或指定**記錄**和[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件之[Mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性值的可用許可權。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|表示唯讀許可權。|  
|**adModeReadWrite**|3|表示讀取/寫入權限。|  
|**adModeRecursive**|0x400000|與其他* \* ShareDeny \* *值（**adModeShareDenyNone**、 **adModeShareDenyWrite**或**adModeShareDenyRead**）搭配使用，以將共用限制傳播到目前**記錄**的所有子記錄。 如果**記錄**沒有任何子系，則不會有任何影響。 如果只與**adModeShareDenyNone**搭配使用，就會產生執行階段錯誤。 不過，與其他值結合時，它可以與**adModeShareDenyNone**搭配使用。 例如，您可以使用 "**adModeRead** " 或**adModeShareDenyNone** or **adModeRecursive**"。|  
|**adModeShareDenyNone**|16|允許其他人以任何許可權開啟連接。 無法拒絕他人的讀取或寫入權限。|  
|**adModeShareDenyRead**|4|防止其他人開啟具有讀取權限的連接。|  
|**adModeShareDenyWrite**|8|防止其他人開啟具有寫入權限的連接。|  
|**adModeShareExclusive**|12|防止其他人開啟連接。|  
|**adModeUnknown**|0|預設值。 指出尚未設定或無法判斷許可權。|  
|**adModeWrite**|2|表示僅限寫入權限。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. ConnectMode. 讀取|  
|AdoEnums. ConnectMode. READWRITE|  
|（沒有對等的 AdoEnums. ConnectMode）|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode。未知|  
|AdoEnums. ConnectMode. WRITE|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Mode 屬性 (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)  
        [Open 方法 (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)  
    :::column-end:::
    :::column:::
        [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)  
        [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::
