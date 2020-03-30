---
title: setAutoCommit 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbf9b18fdc6b590f085b5be6babd64100006163a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975270"
---
# <a name="setautocommit-method-sqlserverconnection"></a>setAutoCommit 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的自動認可模式設定為所指定狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>參數  
 *value*  
  
 **true** 表示啟用連接的自動認可模式，**false** 表示停用。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setAutoCommit 方法是由 java.sql.Connection 介面中的 setAutoCommit 方法指定。  
  
 如果連接處於自動認可模式，則它的所有 SQL 陳述式都會當做個別交易來執行及認可。 否則，它的 SQL 陳述式會分組成許多交易，這些交易會透過 [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 方法或 [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) 方法的呼叫來結束。 根據預設，新的連接會處於自動認可模式。  
  
 當陳述式完成或下一次執行時 (以先發生者為準)，就會進行認可。 如果是傳回 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的陳述式，當擷取結果集的最後一個資料列或是關閉結果集時，該陳述式就會完成。 在進階案例中，除了輸出參數值以外，單一陳述式也可能會傳回多個結果。 在這些案例中，當擷取了所有結果和輸出參數值時，就會發生認可。  
  
 當自動認可模式為 **false** 時，JDBC 驅動程式會在每一次認可之後以隱含方式開始新的交易。  
  
> [!NOTE]  
>  如果在交易期間呼叫這個方法，便會認可交易。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
