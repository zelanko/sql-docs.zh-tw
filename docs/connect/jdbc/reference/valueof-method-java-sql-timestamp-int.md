---
title: valueOf 方法 (java.sql.Timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c13438851fdc543a3567abdc001af5b5b9e726fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68001568"
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 方法 (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根據指定的 java.sql.Timestamp 值以及指出位移 (以分鐘為單位) 的值，建立 **DateTimeOffset** 物件，這個物件表示從 GMT 特定位移的時間點。  
  
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
 傳回 DateTimeOffset 物件，這個物件表示 java.sql.Timestamp 物件在 GMT 給定位移 (以分鐘為單位) 提供的時間點。  
  
## <a name="see-also"></a>另請參閱  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 成員](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
