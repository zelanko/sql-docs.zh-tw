---
title: 使用保留性 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c126385955ce6e9fa9098ec5a09ba115b94ffb0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026203"
---
# <a name="using-holdability"></a>使用保留性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

根據預設，在交易內建立的結果集會在交易認可到資料庫之後或在交易回復時保持開啟。 不過，有時候在已經認可交易之後，讓結果集關閉會很有用。 為了達到此目的，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援使用結果集保留性。

您可以使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法來設定結果集保留性。 使用 setHoldability 方法來設定保留性時，您可以使用 `ResultSet.HOLD_CURSORS_OVER_COMMIT` 或 `ResultSet.CLOSE_CURSORS_AT_COMMIT` 的結果集保留性常數。

JDBC Driver 在建立其中一個陳述式物件時，也支援設定保留性。 使用結果集保留性參數來建立具有多載的陳述式物件時，陳述式物件的保留性必須與連接的保留性相符。 如果它們不相符，就會擲回例外狀況。 這是因為 SQL Server 只會在連接層級支援保留性。

結果集的保留性是 SQLServerConnection 物件的保留性，該物件只有在對伺服器端資料指標建立結果集時，才與結果集建立關聯。 它不適用於用戶端資料指標。 所有具有用戶端資料指標的結果集都一定會具有 `ResultSet.HOLD_CURSORS_OVER_COMMIT` 的保留性值。

如果是伺服器資料指標，則連接至 SQL Server 2005 或更新版本時，設定保留性只會影響即將針對該連接建立之新結果集的保留性。 這表示，設定保留性不會影響先前建立而且已經針對該連線開啟之任何結果集的保留性。

在下列範例中，系統會在執行本機交易 (該交易是由 `try` 區塊中兩個個別陳述式所組成) 時，設定結果集保留性。 這些陳述式是針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中的 Production.ScrapReason 資料表所執行。 首先，此範例會透過將自動認可設定為 `false`，切換成手動交易模式。 一旦停用自動認可模式之後，在應用程式明確呼叫 [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 方法之前，將不會認可任何 SQL 陳述式。 如果擲回例外狀況，catch 區塊中的程式碼便會回復交易。

[!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]

## <a name="see-also"></a>另請參閱

[以 JDBC 驅動程式執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
