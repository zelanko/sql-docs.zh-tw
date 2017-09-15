---
title: "getStatement 方法 (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.getStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dea981b-b4fd-4f8d-954f-e686124627e2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 129fcea59f7ff9555203fe7ced9b51fabade1d83
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getstatement-method-sqlserverresultset"></a>getStatement 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)產生此物件[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Statement getStatement()  
```  
  
## <a name="return-value"></a>傳回值  
 SQLServerStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getStatement 方法是由 java.sql.ResultSet 介面中的 getStatement 方法指定。  
  
 如果結果集由產生的其他方式，例如[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)方法，這個方法會傳回 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
