---
title: "setTime 方法 (SQLServerPreparedStatement) |Microsoft 文件"
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
apiname: SQLServerPreparedStatement.setTime
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b3a83ea3-6636-4096-842b-71b37340fa07
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76d540b51a281f4de1e6f337939c520cf0c64c8a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="settime-method-sqlserverpreparedstatement"></a>setTime 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的時間值。  
  
 開頭為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0 中，這個方法的行為由修改**sendTimeAsDatetime**連接屬性 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊，請參閱[如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|Description|  
|----------|-----------------|  
|[setTime （int，java.sql.Time）](../../../connect/jdbc/reference/settime-method-int-java-sql-time.md)|將指定的參數設定為給定的時間值。|  
|[setTime （int，java.sql.Time，java.util.Calendar）](../../../connect/jdbc/reference/settime-method-int-java-sql-time-java-util-calendar.md)|將指定的參數設定為給定的時間和行事曆值。|  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
