---
title: "valueOf 方法 （java.sql.Timestamp，int） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5bd8228a590f165b9df5df8dcc76798dea81e43
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 方法 (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立**DateTimeOffset**物件表示特定位移的時間點，從 GMT 給定 java.sql.Timestamp 值以及指出位移值，以分鐘為單位。  
  
## <a name="syntax"></a>語法  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>參數  
 *timestamp*  
  
 
          java.sql.Timestamp 值。  
  
 *minutesOffset*  
  
 以分鐘為單位的位移。  
  
## <a name="return-value"></a>傳回值  
 傳回 DateTimeOffset 物件中指定的時間所指定的位移，java.sql.Timestamp 物件分鐘，從 GMT 中表示的點。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

