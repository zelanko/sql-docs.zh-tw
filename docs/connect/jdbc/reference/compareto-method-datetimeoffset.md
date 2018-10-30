---
title: compareTo 方法 (DateTimeOffset) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04f19f08deda9cd42affa0a5ced28255c1bb521b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742926"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 方法 (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  比較這個**DateTimeOffset**物件與另一個**DateTimeOffset**物件根據 GMT 的時間。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>參數  
 您想要與目前執行個體比較的 [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) 值。  
  
## <a name="return-value"></a>傳回值  
 下表描述此方法的傳回值。  
  
|傳回值|Description|  
|------------------|-----------------|  
|0|兩者**DateTimeOffset**物件代表相同的點的時間。|  
|負數|這**DateTimeOffset**物件都代表一個點之前的時間*其他*。|  
|正數|這**DateTimeOffset**物件都代表一個點之後的時間*其他*。|  
  
## <a name="remarks"></a>Remarks  
 當兩個 **DateTimeOffset** 物件有相同的 GMT 時間時，根據位移，物件就沒有其他順序。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
