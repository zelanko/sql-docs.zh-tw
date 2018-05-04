---
title: SQLServerXAResource 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36b5bc655f0ad54a8c326030aa123ef043920a13
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
  
|名稱|Description|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|用來允許緊密結合的 XA 交易，這些交易擁有不同的 XA 分支交易識別碼 (XID)，但是擁有相同的全域交易識別碼 (GTRID)。|  
  
## <a name="inherited-fields"></a>繼承的欄位  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[認可](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|認可給定 Xid 物件所指定的全域交易。|  
|[結束](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|結束代表交易分支執行的工作。|  
|[忘記](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|告知資源管理員要忘記以啟發方式完成的交易分支。|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|取得這個設定的目前交易逾時值[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)物件。|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|判斷目標物件所代表的資源管理員執行個體是否與給定 XAResource 物件所代表的資源管理員執行個體相同。|  
|[準備](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|資源管理員準備給定 Xid 物件所指定之交易的交易認可的要求。|  
|[復原 (recover)](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|從資源管理員取得備妥的交易分支清單。|  
|[復原](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|要求資源管理員回復之前代表交易分支所完成的工作。|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|設定這個目前的交易逾時值[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)物件。|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|代表 Xid 物件中指定的交易分支開始工作。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
