---
title: "getSQLXML 方法 (java.lang.String) |Microsoft 文件"
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
ms.assetid: f56b192a-3255-4215-b552-8e494fbca083
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 21eba6572ba201ae68891cf2c80545d586903290
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlxml-method-javalangstring"></a>getSQLXML 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  為給定的參數名稱的 SQLXML 物件中擷取指定之參數的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 A**字串**，指出參數名稱。  
  
## <a name="return-value"></a>傳回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSQLXML 方法是由 java.sql.CallableStatement 介面中的 getSQLXML 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [getSQLXML 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

