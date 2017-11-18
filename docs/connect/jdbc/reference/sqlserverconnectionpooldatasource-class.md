---
title: "SQLServerConnectionPoolDataSource 類別 |Microsoft 文件"
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
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82712fa541d958527c409d5a347b69f37d5e642f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表連接集區管理員的實體資料庫連接。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **實作：** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>備註  
 SQLServerConnectionPoolDataSource 通常會用於 Java Application Server 環境支援內建連接共用，而且需要來提供實體連接，例如 Java Platform Enterprise Edition (Java ConnectionPoolDataSourceEE) 應用程式伺服器提供 JDBC 3.0 API 規格連接共用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

