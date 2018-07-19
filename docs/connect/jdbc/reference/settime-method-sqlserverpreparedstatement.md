---
title: setTime 方法 (SQLServerPreparedStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTime
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3a83ea3-6636-4096-842b-71b37340fa07
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7719173f1aaeafcdfed8adf89837dfd040a41620
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32844593"
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
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
