---
title: "getClientConnectionID 方法 (SQLServerConnection) |Microsoft 文件"
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
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be59e3cb669c9ac62b11901cc548a8223dd9e2f4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>getClientConnectionID 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取得最新連接嘗試的連接識別碼，不論嘗試成功或失敗。  
  
## <a name="syntax"></a>語法  
  
```vb  
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>傳回值  
 16 位元組 GUID，代表最新連接嘗試的連接識別碼。 如果起始連接要求以及預先登入交握之後發生失敗，則為 NULL。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 如需存取擴充的事件記錄檔中的診斷資訊的詳細資訊，請參閱[存取擴充的事件記錄檔中的診斷資訊](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
 下列範例會示範如何取得連接識別碼：  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 下列範例會示範另一種取得連接識別碼的方式：  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("…");  
ds.setPassword("…");  
ds.setServerName("…");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID** ，連接的伺服器版本為何，都會運作，但擴充的事件記錄檔以及有關連接性信號緩衝錯誤的項目將不會出現在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]2008 R2 及更早版本。  
  
 如果記錄連接識別碼的擴充事件已啟用，您就可以在擴充事件記錄檔中找出連接識別碼，以便查看失敗是否位於伺服器。 您也可以在連接信號緩衝區中找到的連接識別碼 ([連接 SQL Server 2008 中與連接信號緩衝區疑難排解](http://go.microsoft.com/fwlink/?LinkId=207752)) 針對特定連接錯誤。 如果連接識別碼不在連接信號緩衝區中，您就可以假設發生網路錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
