---
title: getHoldability 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cf27049e45c8e52c8a63a419327f377dd1f558f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841396"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的保留性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>傳回值  
 **int** 值，包含下列其中一個保留性等級：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getHoldability 方法是由 java.sql.ResultSet 介面中的 getHoldability 方法指定。  
  
 為了設定結果集保留性，應用程式可能會使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法。 在呼叫 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法、建立陳述式物件及其結果集物件，以及執行該陳述式之後，應用程式可能需要再次變更其保留性。  
  
 如果是伺服器資料指標，則連接至 SQL Server 2005 或更新版本時，設定保留性只會影響即將針對該連接建立之新結果集的保留性。 不過，在 SQL Server 2000 中，設定保留性則會影響現有結果集以及即將針對該連接建立之新結果集的保留性。  
  
 當重設保留性，而且 getHoldability 方法呼叫先前建立的結果集物件，這個方法所傳回的值可能會與下列方法所傳回的保留性值不同： Statement.getResultSetHoldabilityConnection.getHoldability 或 DatabaseMetaData.getResultSetHoldability。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
