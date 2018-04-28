---
title: getServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04c1abc48831d9dbb2501bc803b53568f64b3fd4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 傳回的值**serverPreparedStatementDiscardThreshold**連接屬性。 此設定會控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 如果設定為 < = 1，取消準備備妥的陳述式關閉上立即執行動作。 如果它設定為 > 1，這些呼叫會一起批次處理以避免太過頻繁呼叫 sp_unprepare 的額外負荷。 呼叫 getDefaultServerPreparedStatementDiscardThreshold() 可以變更這個選項的預設值。

## <a name="syntax"></a>語法  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>傳回值
 **Int** ，其中包含值**serverPreparedStatementDiscardThreshold**連接屬性。

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 這個方法是從 JDBC 驅動程式版本 6.4 可用且向外。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
