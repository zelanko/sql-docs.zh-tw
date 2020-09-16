---
description: getServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource)
title: getServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e779955f77be3891bb3f7479b4a40fb30b3d56ac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434540"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **serverPreparedStatementDiscardThreshold** 連接屬性的值。 此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少個未完成的備妥陳述式捨棄動作 (sp_unprepare) 尚未完成。 當設定為 <= 1 時，備妥陳述式一結束就會立即執行未準備動作。 如果此值設定為 > 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷。

  
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
  
  
