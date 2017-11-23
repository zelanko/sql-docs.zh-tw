---
title: "getColumnClassName 方法 (SQLServerResultSetMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSetMetaData.getColumnClassName
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 2c118790-5dd2-4b10-93b6-7f065ee324ce
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e398d757b7c967713f4fb4f418ac397e5f09d21
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getcolumnclassname-method-sqlserverresultsetmetadata"></a>getColumnClassName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回時，其執行個體進行製造的 Java 類別的完整限定名稱[getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)類別呼叫以擷取資料行的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getColumnClassName(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 A**字串**其中包含完整類別名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getColumnClassName 方法是由 java.sql.ResultSetMetaData 介面中 getColumnClassName 方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
