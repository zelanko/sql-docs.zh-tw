---
title: "了解交易 |Microsoft 文件"
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
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efaa7480d3a42048fe4ba625471383ae0c127034
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-transactions"></a>了解交易
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  交易是併入邏輯工作單位的作業群組。 它們是用來控制及維護交易中每個動作的一致性與完整性，儘管系統可能會發生錯誤。  
  
 與[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，交易可以是本機或分散式。 交易也可使用隔離等級。 如需 JDBC 驅動程式支援的隔離等級的詳細資訊，請參閱[了解隔離等級](../../connect/jdbc/understanding-isolation-levels.md)。  
  
 應用程式應該使用 Transact-SQL 陳述式或 JDBC Driver 所提供的方法來控制交易，但不可同時使用這兩者。 針對相同的交易同時使用 Transact-SQL 陳述式和 JDBC API 方法可能會導致問題發生，例如無法依照預期方式認可交易、交易已認可或回復但新的交易非預期地啟動，或者發生「無法繼續交易」例外狀況。  
  
## <a name="using-local-transactions"></a>使用本機交易  
 當交易為單一階段交易時，便會視為本機交易，該交易是由資料庫直接處理。 JDBC 驅動程式使用的各種方法來支援本機交易[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別，包括[setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)，[認可](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)，和[復原](../../connect/jdbc/reference/rollback-method.md)。 本機交易通常是由應用程式明確管理，或由 Java Platform Enterprise Edition (Java EE) 應用程式伺服器自動管理。  
  
 下列範例會在兩個個別陳述式組成的本機交易`try`區塊。 針對中的 Production.ScrapReason 資料表執行陳述式[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫中，便會認可它們會擲回任何例外狀況。 中的程式碼`catch`區塊會回復交易發生例外狀況。  
  
 [!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]  
  
## <a name="using-distributed-transactions"></a>使用分散式交易  
 分散式交易會在兩個或以上的網路資料庫上更新資料，並同時保留重要的不可部分完成、一致、獨立且持久的 (ACID) 交易處理屬性。 分散式交易支援已新增至 JDBC 2.0 Optional API 規格中的 JDBC API。 分散式交易的管理通常是由 Java EE 應用程式伺服器環境中的 Java Transaction Service (JTS) 交易管理員自動執行。 不過，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援任何 Java Transaction API (JTA) 相容之交易管理員下的分散式的交易。  
  
 與緊密整合，JDBC 驅動程式[!INCLUDE[msCoName](../../includes/msconame_md.md)]分散式交易協調器 (MS DTC) 來提供真正的分散式交易支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 MS DTC 是所提供的分散式的交易機制[!INCLUDE[msCoName](../../includes/msconame_md.md)]如[!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows 系統。 MS DTC 使用來自經過驗證的交易處理技術[!INCLUDE[msCoName](../../includes/msconame_md.md)]以支援 XA 功能，例如完整的二階段分散式的認可通訊協定和分散式交易的復原。  
  
 如需如何使用分散式的交易的詳細資訊，請參閱[了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [使用 JDBC Driver 執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
