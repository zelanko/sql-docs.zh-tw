---
title: 了解交易 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c5e05c40ffcdcffed884cd5d10dc5219b59f25f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812007"
---
# <a name="understanding-transactions"></a>了解交易

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

交易是併入邏輯工作單位的作業群組。 它們是用來控制及維護交易中每個動作的一致性與完整性，儘管系統可能會發生錯誤。

使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，交易可以是本機或分散式。 交易也可使用隔離等級。 如需有關 JDBC 驅動程式支援的隔離等級的詳細資訊，請參閱 <<c0> [ 了解隔離等級](../../connect/jdbc/understanding-isolation-levels.md)。

應用程式應該使用 Transact-SQL 陳述式或 JDBC Driver 所提供的方法來控制交易，但不可同時使用這兩者。 針對相同的交易同時使用 Transact-SQL 陳述式和 JDBC API 方法可能會導致問題發生，例如無法依照預期方式認可交易、交易已認可或回復但新的交易非預期地啟動，或者發生「無法繼續交易」例外狀況。

## <a name="using-local-transactions"></a>使用本機交易

當交易為單一階段交易時，便會視為本機交易，該交易是由資料庫直接處理。 JDBC 驅動程式 使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的各種方法以支援本機交易，包括 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)、[commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 與 [rollback](../../connect/jdbc/reference/rollback-method.md)。 本機交易通常是由應用程式明確管理，或由 Java Platform Enterprise Edition (Java EE) 應用程式伺服器自動管理。

下列範例會執行 `try` 區塊中由二個個別陳述式組成的本機交易。 這些陳述式是針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中的 Production.ScrapReason 資料表執行，若沒有發生任何例外狀況，便會認可它們。 如果擲回例外狀況，`catch` 區塊中的程式碼便會復原交易。

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>使用分散式交易

分散式交易會在兩個或以上的網路資料庫上更新資料，並同時保留重要的不可部分完成、一致、獨立且持久的 (ACID) 交易處理屬性。 分散式交易支援已新增至 JDBC 2.0 Optional API 規格中的 JDBC API。 分散式交易的管理通常是由 Java EE 應用程式伺服器環境中的 Java Transaction Service (JTS) 交易管理員自動執行。 然而，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援任何符合 Java Transaction API (JTA) 規範之交易管理員下的分散式交易。

JDBC 驅動程式與 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 分散式交易協調器 (MS DTC) 密切整合，以提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實際的分散式交易支援。 MS DTC 是一種由 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 針對 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 系統所提供的分散式交易機制。 MS DTC 使用來自 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 經過驗證的交易處理技術以支援 XA 功能，例如完整的二階段分散式認可通訊協定，以及分散式交易的復原。

如需如何使用分散式的交易的詳細資訊，請參閱[了解 XA 交易](../../connect/jdbc/understanding-xa-transactions.md)。

## <a name="see-also"></a>另請參閱

[使用 JDBC Driver 執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
