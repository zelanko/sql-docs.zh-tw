---
title: setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b1511a2fe703a21dd61050e8bd608044caad8b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 指定特定的連接執行個體的行為。 此設定會控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 當設定為 < = 1 取消-準備關閉已備妥的陳述式會立即執行動作。 如果值設定為 > 1 這些呼叫會一起批次處理以避免太過頻繁呼叫 sp_unprepare 的額外負荷。


## <a name="syntax"></a>語法  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>參數  
 *thresholdValue*  
 
 新值**serverPreparedStatementDiscardThreshold**連接屬性。  
 
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 這個方法是從 JDBC 驅動程式版本 6.4 可用且向外。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
