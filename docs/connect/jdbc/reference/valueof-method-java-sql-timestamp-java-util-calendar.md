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
manager: jroth
ms.openlocfilehash: 3e2d977647153ab74299a6b6f002ec33d3003558
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802543"
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
  
  
