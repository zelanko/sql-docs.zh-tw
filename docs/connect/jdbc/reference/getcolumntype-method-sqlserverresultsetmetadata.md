---
title: "getColumnType 方法 (SQLServerResultSetMetaData) |Microsoft 文件"
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
- SQLServerResultSetMetaData.getColumnType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81815a41-9265-4574-a4d8-f6341a68d9fd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad090a3ad5377be43f0c91febb79cfbfc56b5330
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getcolumntype-method-sqlserverresultsetmetadata"></a>getColumnType 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之資料行的 SQL 型別。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getColumnType(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出 java.sql.Types 內定義的 JDBC 型別。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getColumnType 方法是由 java.sql.ResultSetMetaData 介面中 getColumnType 方法指定。  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 驅動程式 3.0 在 DATA_TYPE 資料行中有行為變更。 請參閱[SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)如需詳細資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

