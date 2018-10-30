---
title: valueOf 方法 (java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd94495081d99521758747f174268d2163cf67e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742736"
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf 方法 (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根據所指定 java.sql.Timestamp 值以及指出位移的 java.util.Calendar 值，建立 **DateTimeOffset** 物件，這個物件表示從 GMT 特定位移的時間點。  
  
## <a name="syntax"></a>語法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>參數  
 *timestamp*  
  
 java.sql.Timestamp 值。  
  
 *calendar*  
  
 位移值。  日期和時間元件*行事曆*將根據*時間戳記*值。  
  
## <a name="return-value"></a>傳回值  
 傳回 DateTimeOffset 物件，表示在給定 java.sql.Timestamp 物件在指定的 java.util.Calendar 物件之時區的時間內的點。  
  
## <a name="remarks"></a>Remarks  
 這個方法也會設定點 java.util.Calendar 物件 java.sql.Timestamp 物件所指定的時間。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
