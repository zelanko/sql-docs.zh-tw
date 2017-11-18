---
title: "getBytes 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d0dac7f-7f39-47a2-953e-80ab03688d82
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2d4a2eba7c1ec403d8079188c8cdc8a874bf7cdf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-javalangstring"></a>getBytes 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過給定的參數名稱，擷取指定之參數的值來當做位元組值的陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public byte[] getBytes(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數名稱。  
  
## <a name="return-value"></a>傳回值  
 陣列**位元組**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 在舊版的[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]，您可以使用 SQLServerCallableStatement.getBytes 來轉換位元組陣列之間的值和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別**日期**，**時間**， **datetime2**，或**datetimeoffset**。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
 GetBytes 方法 java.sql.CallableStatement 介面中所指定這個 getBytes 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getBytes 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

