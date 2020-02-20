---
title: getServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 3f91b75b5c70029d53582b8b6ed4655485fd3fcf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979901"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **serverPreparedStatementDiscardThreshold** 連接屬性的值。 此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少未完成的未完成備妥陳述式捨棄動作 (sp_unprepare)。 當設定為 <= 1 時，備妥陳述式一結束就會立即執行未準備動作。 如果此值設定為 > 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷。

  
## <a name="syntax"></a>語法  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 **serverPreparedStatementDiscardThreshold** 連接屬性的 **int** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 從 JDBC 驅動程式 6.4 版開始，可以使用此方法。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
