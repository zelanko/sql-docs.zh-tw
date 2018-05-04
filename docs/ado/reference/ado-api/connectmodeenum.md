---
title: ConnectModeEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f35019573f17e49fea3bdec7bfe6afc17b844f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connectmodeenum"></a>ConnectModeEnum
指定在修改資料的可用權限[連接](../../../ado/reference/ado-api/connection-object-ado.md)、 開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)，或指定的值[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性**記錄**和[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|表示唯讀權限。|  
|**adModeReadWrite**|3|表示讀取/寫入權限。|  
|**adModeRecursive**|0x400000|用於搭配其他*\*ShareDeny\** 值 (**adModeShareDenyNone**， **adModeShareDenyWrite**，或**adModeShareDenyRead**) 傳播至所有子記錄的目前的共用限制**記錄**。 如果有任何影響**記錄**並沒有任何子系。 如果搭配使用，就會產生執行階段錯誤**adModeShareDenyNone**只。 不過，它可以搭配**adModeShareDenyNone**與其他值結合時。 例如，您可以使用 「**adModeRead**或者**adModeShareDenyNone**或者**adModeRecursive**"。|  
|**adModeShareDenyNone**|16|可讓其他人開啟與任何權限的連線。 無法拒絕他人的讀取或寫入權限。|  
|**adModeShareDenyRead**|4|防止他人的讀取權限開啟連接。|  
|**adModeShareDenyWrite**|8|防止其他人具有寫入權限開啟連接。|  
|**adModeShareExclusive**|12|防止其他人開啟連接。|  
|**adModeUnknown**|0|預設值。 表示尚未設定的權限，或無法判斷。|  
|**adModeWrite**|2|指出唯寫的權限。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|（AdoEnums.ConnectMode.RECURSIVE 沒有對等用法)|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Mode 屬性 (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open 方法 (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
