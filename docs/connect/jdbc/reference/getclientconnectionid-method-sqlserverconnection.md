---
title: getClientConnectionID 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa6954248b747cfd08789fa6f2e73ebc1e4befba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730016"
---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>getClientConnectionID 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取得最新連接嘗試的連接識別碼，不論嘗試成功或失敗。  
  
## <a name="syntax"></a>語法  
  
``` 
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>傳回值  
 16 位元組 GUID，代表最新連接嘗試的連接識別碼。 如果起始連接要求以及預先登入交握之後發生失敗，則為 NULL。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 如需有關存取擴充的事件記錄檔中的診斷資訊的詳細資訊，請參閱[存取擴充的事件記錄檔中的診斷資訊](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
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
  
 不論您所連線的伺服器版本為何，**getClientConnectionID** 都會運作，但是擴充事件記錄檔以及連線信號緩衝區錯誤的相關項目不會出現在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 R2 和先前版本中。  
  
 如果記錄連接識別碼的擴充事件已啟用，您就可以在擴充事件記錄檔中找出連接識別碼，以便查看失敗是否位於伺服器。 此外，您也可以針對特定連線錯誤，在連線信號緩衝區中找出連線識別碼 ([透過連線信號緩衝區針對 SQL Server 2008 中的連線問題進行疑難排解](http://go.microsoft.com/fwlink/?LinkId=207752))。 如果連接識別碼不在連接信號緩衝區中，您就可以假設發生網路錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
