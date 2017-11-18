---
title: "allTablesAreSelectable 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
- SQLServerDatabaseMetaData.allTablesAreSelectable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb340450-45a7-49c8-84bc-1b9dd5ee842f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d605d9c9725c5819af595115292e1cc3752ec0c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="alltablesareselectable-method-sqlserverdatabasemetadata"></a>allTablesAreSelectable 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前使用者是否有權限來使用所傳回的所有資料表[getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) SELECT 陳述式中的方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean allTablesAreSelectable()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果使用者有權限可使用所有資料表。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 allTablesAreSelectable 方法是由 java.sql.DatabaseMetaData 介面中 allTablesAreSelectable 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

