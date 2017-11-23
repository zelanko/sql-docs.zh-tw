---
title: "使用保留性 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c59212d8e0ebdf6eb57ecdc737582d73998124a5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="using-holdability"></a>使用保留性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  根據預設，在交易內建立的結果集會在交易認可到資料庫之後或在交易回復時保持開啟。 不過，有時候在已經認可交易之後，讓結果集關閉會很有用。 若要這樣做，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援使用結果集保留性。  
  
 可以透過設定結果集保留性[setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 當使用 setHoldability 方法設定保留性，結果集保留性 ResultSet.HOLD_CURSORS_OVER_COMMIT 常數或 ResultSet.CLOSE_CURSORS_AT_COMMIT 可用。  
  
 JDBC Driver 在建立其中一個陳述式物件時，也支援設定保留性。 使用結果集保留性參數來建立具有多載的陳述式物件時，陳述式物件的保留性必須與連接的保留性相符。 如果它們不相符，就會擲回例外狀況。 這是因為 SQL Server 只有連接層級才支援保留性。  
  
 結果集保留性是 SQLServerConnection 物件的結果集的結果集建立時的時間，對伺服器端資料指標只在有關聯的保留性。 它不適用於用戶端資料指標。 所有具有用戶端資料指標結果集一定會 ResultSet.HOLD_CURSORS_OVER_COMMIT 的保留性值。  
  
 如果是伺服器資料指標，則連接至 SQL Server 2005 或更新版本時，設定保留性只會影響即將針對該連接建立之新結果集的保留性。 這表示，設定保留性不會影響先前建立而且已經針對該連接開啟之任何結果集的保留性。 不過，在 SQL Server 2000 中，設定保留性則會影響現有結果集以及即將針對該連接建立之新結果集的保留性。  
  
 下列範例中，在執行中的兩個個別陳述式所組成的本機交易時設定結果集保留性`try`區塊。 針對中的 Production.ScrapReason 資料表執行陳述式[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫。 首先，範例會切換成手動交易模式設定為自動認可**false**。 一旦停用自動認可模式之後，任何 SQL 陳述式將會認可直到應用程式呼叫[認可](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)方法明確。 如果擲回例外狀況，catch 區塊中的程式碼便會回復交易。  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>請參閱＜  
 [使用 JDBC Driver 執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
