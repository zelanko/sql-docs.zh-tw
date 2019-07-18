---
title: 使用儲存點 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bd9903438f2bc52d6f3ac87bfc6628bf08e3b9f1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798628"
---
# <a name="using-savepoints"></a>使用儲存點

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

儲存點提供了復原部份交易的機制。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內，您可以使用 SAVE TRANSACTION savepoint_name 陳述式來建立儲存點。 稍後，您可以執行 ROLLBACK TRANSACTION savepoint_name 陳述式來回復到儲存點，而不是回復到交易開始。

如果所處環境不太可能發生錯誤，儲存點會很有幫助。 不常發生錯誤時，使用儲存點來回復交易的一部份，會比在進行更新之前，需測試每筆交易以查看更新是否有效來得更有效率。 更新與回復都是高成本的作業，因此儲存點只有在遇到錯誤的可能性不高，且事前檢查更新可用性的成本相當高的情形下才有效率。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會透過 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) 方法，支援儲存點的使用。 使用 setSavepoint 方法，您可以在目前交易內建立一個已命名或未命名的儲存點，此方法將傳回 [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) 物件。 在交易內可建立多個儲存點。 若要使交易回復到指定的儲存點，您可以傳遞 SQLServerSavepoint 物件給 [rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) 方法。

在下列範例中，執行本機交易時會使用儲存點，此交易是由 `try` 區塊的兩個個別陳述式所組成。 這些陳述式是針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中的 Production.ScrapReason 資料表執行，並使用儲存點來回復第二個陳述式。 這樣會造成只有第一個陳述式認可到資料庫。

[!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]

## <a name="see-also"></a>另請參閱

[使用 JDBC Driver 執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
