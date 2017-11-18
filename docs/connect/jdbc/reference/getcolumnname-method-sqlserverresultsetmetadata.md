---
title: "getColumnName 方法 (SQLServerResultSetMetaData) |Microsoft 文件"
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
- SQLServerResultSetMetaData.getColumnName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0330ca1d-5e24-4ce3-9d2a-b931f20a0fcf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a27af3fe868fbbe62d6587d8b3f2183e39845fd6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getcolumnname-method-sqlserverresultsetmetadata"></a>getColumnName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取得指定之資料行的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getColumnName(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含資料行名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getColumnName 方法是由 java.sql.ResultSetMetaData 介面中 getColumnName 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

