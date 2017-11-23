---
title: "getURL 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
apiname: SQLServerDatabaseMetaData.getURL
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cbc569dbd45ede9429b6299e2f37d7f7a5cb269c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>getURL 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫的 URL。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**包含 URL。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getURL 方法是由 java.sql.DatabaseMetaData 介面中 getURL 方法指定。  
  
 當使用[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]與[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫，這個方法會傳回**字串**值，包含下列資訊：  
  
-   URL 值，"jdbc:sqlserver://"  
  
-   選擇性的連接屬性，例如**serverName**， **instanceName**，和**通訊埠編號**  
  
-   其他連接屬性設定由使用者和所有的連接屬性不可空白或非 null 驅動程式預設值除了**userName**，**密碼**，和**integratedSecurity**.  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
