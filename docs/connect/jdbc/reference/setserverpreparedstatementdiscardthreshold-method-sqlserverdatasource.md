---
title: setServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28c3a442f89813a4ce93ded9035c1bc16f9e47c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972839"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>setServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定 serverPreparedStatementDiscardThreshold 連接屬性的值。 此設定可控制在執行清除伺服器上未完成的控制碼之前, 每個連接的未完成準備語句捨棄動作 (sp_unprepare)。 當設定為 < = 1 時, unprepare 動作會在備妥的語句關閉時立即執行。 如果值設定為 > 1, 則會將這些呼叫批次處理在一起, 以避免太常呼叫 sp_unprepare 的額外負荷
 
## <a name="syntax"></a>語法  
  
```
public void setServerPreparedStatementDiscardThreshold(int enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>參數  
 *serverPreparedStatementDiscardThreshold*  
  
 **ServerPreparedStatementDiscardThreshold**連接屬性的新值。  

## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 這個方法可從 JDBC 驅動程式6.4 版和之後版本取得。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
