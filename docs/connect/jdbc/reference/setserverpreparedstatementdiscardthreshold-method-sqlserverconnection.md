---
description: setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
title: setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca004a1eeb2e0446126673f4d500cdef092915dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458331"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 指定特定連線執行個體的行為。 此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少個未完成的備妥陳述式捨棄動作 (sp_unprepare) 尚未完成。 當設定為 <= 1 時，準備陳述式一結束就會立即執行未準備動作。 如果值設定為 > 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷。


## <a name="syntax"></a>語法  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>參數  
 *thresholdValue*  
 
 **serverPreparedStatementDiscardThreshold** 連接屬性的新值。  
 
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 從 JDBC 驅動程式 6.4 版開始，可以使用此方法。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
