---
title: "executeQuery 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.executeQuery (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 610205c2-6bcd-426c-ad6f-9682551efdec
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ad4fe32e78984773325df4f34b3762f61a9924d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="executequery-method-javalangstring"></a>executeQuery 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行給定的 SQL 陳述式，並傳回單一[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.ResultSet executeQuery(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 A**字串**，其中包含 SQL 陳述式。  
  
## <a name="return-value"></a>傳回值  
 
          SQLServerResultSet 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 executeQuery 方法是由 java.sql.Statement 介面中的 executeQuery 方法來指定。  
  
 這個方法會覆寫[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法中找到[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)類別。  
  
 呼叫這個方法會導致例外狀況，因為在建立物件時指定 SQLServerPreparedStatement 物件的 SQL 陳述式。  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)如果給定的 SQL 陳述式產生單一以外的任何項目，會擲回[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="see-also"></a>另請參閱  
 [executeQuery 方法 &#40;SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
