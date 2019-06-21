---
title: getSQLStateType 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 55079e30c2f8908153cc708aca699e77aef41261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66774180"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出由 SQLException.getSQLState 方法傳回的 SQLSTATE 是 X/Open (現在稱為 Open Group)、SQL CLI、SQL99 (JDBC 3.0) 或 SQL:2003 (JDBC 4.0)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>傳回值  
 指出 SQLSTATE 類型的 **int**，可能是下列其中一個值：  
  
-   針對 Java Runtime Environment 5.0 版： 如果**xopenStates**連接屬性設定為 **，則為 true**，這個方法會傳回 DatabaseMetaData.sqlStateXOpen。 否則，DatabaseMetaData.sqlStateSQL99。  
  
-   針對 Java Runtime Environment 6.0 版： 如果**xopenStates**連接屬性設定為 **，則為 true**，這個方法會傳回 DatabaseMetaData.sqlStateXOpen。 否則，DatabaseMetaData.sqlStateSQL。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSQLStateType 方法是由 java.sql.DatabaseMetaData 介面中 getSQLStateType 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
