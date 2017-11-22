---
title: "doesMaxRowSizeIncludeBlobs 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
apiname: SQLServerDatabaseMetaData.doesMaxRowSizeIncludeBlobs
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 0c90a7a7-5a59-4858-bb26-3e725d8611d7
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30f0afda970fb27c762c57d9ba3c81387829c0b2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="doesmaxrowsizeincludeblobs-method-sqlserverdatabasemetadata"></a>doesMaxRowSizeIncludeBlobs 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取是否傳回值[getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md)方法包括 SQL 資料類型 LONGVARCHAR 和 LONGVARBINARY。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean doesMaxRowSizeIncludeBlobs()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果傳回的值包括資料類型。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 doesMoxRowSizeIncludeBlobs 方法是由 java.sql.DatabaseMetaData 介面中 doesMoxRowSizeIncludeBlobs 方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
