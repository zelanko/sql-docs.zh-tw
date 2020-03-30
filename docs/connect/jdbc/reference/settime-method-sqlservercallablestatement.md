---
title: setTime 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTime
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04ea83b2-db5e-4b46-b016-9e496363827e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81205764a663930ab2d555c0f231448c6cae4099
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972465"
---
# <a name="settime-method-sqlservercallablestatement"></a>setTime 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的時間值。  
  
 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 驅動程式 3.0 開始，這個方法的行為是由 **sendTimeAsDatetime** 連線屬性 ([設定連線屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 所修改。  
  
 如需詳細資訊，請參閱[設定 java.sql.Time 值如何傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|描述|  
|----------|-----------------|  
|[setTime (java.lang.String, java.sql.Time)](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time.md)|將指定的參數設定為給定的時間值。|  
|[setTime (java.lang.String, java.sql.Time, java.util.Calendar)](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time-java-util-calendar.md)|將指定的參數設定為給定的時間和行事曆值。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 方法](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
