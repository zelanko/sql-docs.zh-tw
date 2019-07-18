---
title: SQLServerXAConnection 成員 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1399700551402870a4eeb7cd2339a7a2e937468f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797487"
---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(繼承自 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 註冊指定的事件接聽程式，如此一來，當這個 Connection 物件上發生事件時，它就可以收到通知。|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(繼承自 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 關閉這個 Connection 物件所代表的實體連接。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(繼承自 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 建立這個 Connection 物件所代表實體連接的物件控制代碼。|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|擷取 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件，交易管理員將會使用它來管理參與分散式交易中的這個 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 物件。|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(繼承自 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 移除指定的事件接聽程式。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|javax.sql.PooledConnection|addConnectionEventListener, close, getConnection, removeConnectionEventListener|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 類別](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
