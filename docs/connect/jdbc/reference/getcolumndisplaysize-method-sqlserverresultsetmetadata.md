---
title: "getColumnDisplaySize 方法 (SQLServerResultSetMetaData) |Microsoft 文件"
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
- SQLServerResultSetMetaData.getColumnDisplaySize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 21c25443-bd2b-4b60-9798-4efe2c158952
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 10eb09f395c661e7cc46629662d62e43bd937f05
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getcolumndisplaysize-method-sqlserverresultsetmetadata"></a>getColumnDisplaySize 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回指定之資料行的正常最大寬度 (以字元為單位)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getColumnDisplaySize(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 **Int**表示的最大寬度。 如果寬度未知，則會傳回 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getColumnDisplaySize 方法是由 java.sql.ResultSetMetaData 介面中 getColumnDisplaySize 方法指定。  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 驅動程式 3.0 在 COLUMN_SIZE 資料行中有行為變更。 請參閱[SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)如需詳細資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

