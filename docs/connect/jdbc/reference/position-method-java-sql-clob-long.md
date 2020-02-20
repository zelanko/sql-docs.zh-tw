---
title: position 方法 (java.sql.Clob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.sql.Clob, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2fb34d5-1d34-4764-a795-712d9c6aa313
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b9af31e7701633e7cd73e8aaf0eb498b26c02c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976414"
---
# <a name="position-method-javasqlclob-long"></a>position 方法 (java.sql.Clob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  依據給定的開始位置，傳回 CLOB 內指定之 CLOB 物件的字元位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
public long position(java.sql.Clob searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>參數  
 *searchstr*  
  
 要搜尋的子字串。  
  
 *start*  
  
 開始搜尋的位置。 第一個位置是 1。  
  
## <a name="return-value"></a>傳回值  
 子字串的出現位置，如果未出現，則為 -1。 第一個位置是 1。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 position 方法是由 java.sql.Clob 介面中的 position 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [position 方法 &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
