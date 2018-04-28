---
title: 使用儲存點 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
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
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dccc8739a02fa478c153bbbe1702b925942f8efd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-savepoints"></a>使用儲存點
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  儲存點提供了復原部份交易的機制。 內[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以使用 SAVE TRANSACTION savepoint_name 陳述式來建立儲存點。 稍後，您可以執行 ROLLBACK TRANSACTION savepoint_name 陳述式來回復到儲存點，而不是回復到交易開始。  
  
 如果所處環境不太可能發生錯誤，儲存點會很有幫助。 不常發生錯誤時，使用儲存點來回復交易的一部份，會比在進行更新之前，需測試每筆交易以查看更新是否有效來得更有效率。 更新與回復都是高成本的作業，因此儲存點只有在遇到錯誤的可能性不高，且事前檢查更新可用性的成本相當高的情形下才有效率。  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援儲存點，透過使用[setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 SetSavepoint 方法，您可以使用建立具名或未命名的儲存點，在目前的交易中，則方法會傳回[SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md)物件。 在交易內可建立多個儲存點。 若要以給定的儲存點上回復交易，您可以 SQLServerSavepoint 物件傳遞至[rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md)方法。  
  
 在下列範例中，儲存點時，會使用執行中的兩個個別陳述式所組成的本機交易`try`區塊。 針對中的 Production.ScrapReason 資料表執行陳述式[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫和儲存點來回復第二個陳述式。 這樣會造成只有第一個陳述式認可到資料庫。  
  
 [!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
