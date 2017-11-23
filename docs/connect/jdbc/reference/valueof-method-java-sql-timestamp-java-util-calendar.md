---
title: "valueOf 方法 （java.sql.Timestamp，java.util.Calendar） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 138a53f22791390600ed21e535a7c26597f46321
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf 方法 (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立**DateTimeOffset**物件表示特定位移的時間點，從 GMT 給定 java.sql.Timestamp 值以及指出位移的 java.util.Calendar 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>參數  
 *timestamp*  
  
 
          java.sql.Timestamp 值。  
  
 *行事曆*  
  
 位移值。  日期和時間元件*行事曆*將根據*時間戳記*值。  
  
## <a name="return-value"></a>傳回值  
 傳回 DateTimeOffset 物件，代表在給定 java.sql.Timestamp 物件在給定的 java.util.Calendar 物件之時區的時間點。  
  
## <a name="remarks"></a>備註  
 這個方法也會設定為點 java.util.Calendar 物件 java.sql.Timestamp 物件所提供的時間。  
  
## <a name="see-also"></a>請參閱＜  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
