---
title: "getSystemFunctions 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
apiname: SQLServerDatabaseMetaData.getSystemFunctions
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6d390ec5-9ee2-49c4-b661-a93b55691dd1
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d11a25ab205f3284c1fe227ebd1ba0fa5ae9fb5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getsystemfunctions-method-sqlserverdatabasemetadata"></a>getSystemFunctions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫可用之系統函式的逗號分隔清單。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getSystemFunctions()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含系統函式清單。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSystemFunctions 方法是由 java.sql.DatabaseMetaData 介面中 getSystemFunctions 方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
