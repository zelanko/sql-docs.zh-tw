---
title: "getBigDecimal 方法 (java.lang.String) |Microsoft 文件"
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
- SQLServerCallableStatement.getBigDecimal (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d0b29b48-9663-4de4-9fc2-82bc30e44aed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 815ed2b2460a4b492868074f5e11e607f0effe70
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbigdecimal-method-javalangstring"></a>getBigDecimal 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  配合給定的參數名稱來擷取指定之參數的值當做 java.math.BigDecimal (具有完整有效位數)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數名稱。  
  
## <a name="return-value"></a>傳回值  
 BigDecimal 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBigDecimal 方法 java.sql.CallableStatement 介面中所指定這個 getBigDecimal 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getBigDecimal 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

