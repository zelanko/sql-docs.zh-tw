---
title: SQLServerXAConnection 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 188140965c0040f8454156555b71adbd2fe89ce9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(繼承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 註冊指定的事件接聽程式，以便將在此連接物件上發生事件時通知。|  
|[關閉](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(繼承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 關閉這個連線物件所代表的實體連接。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(繼承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 建立這個連線物件所代表的實體連接的物件控制代碼。|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|擷取[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)物件的交易管理員將用來管理的參與[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)分散式交易中的物件。|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(繼承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 移除指定的事件接聽程式。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 類別](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
