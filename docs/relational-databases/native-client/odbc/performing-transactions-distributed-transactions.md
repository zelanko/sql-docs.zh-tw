---
title: 建立分散式的交易 |Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e3eb73528800d45daf0ea8b68ae94536f63c25df
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585483"
---
# <a name="create-a-distributed-transaction"></a>建立分散式的交易

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

分散式的交易可以針對不同的 Microsoft SQL 系統中建立，以不同的方式。

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 驅動程式會呼叫 SQL Server 內部 MSDTC

Microsoft Distributed Transaction Coordinator (MSDTC) 可讓擴充的應用程式或_散發_跨兩個或多個執行個體的交易[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 即使兩個執行個體裝載於不同的電腦上的運作方式的分散式的交易。

MSDTC 已安裝適用於 Microsoft SQL Server 內部部署，但不適用於 Microsoft Azure SQL Database 雲端服務。

MSDTC 會呼叫 SQL Server Native Client 驅動程式 「 開放式資料庫連接 (ODBC)，當您C++計劃管理分散式的交易。 Native Client ODBC 驅動程式有相容以開啟群組分散式交易處理 (DTP) 標準的 XA 交易管理員。 此合規性所需的 MSDTC。 一般而言，所有交易管理命令會透過此 Native Client ODBC 驅動程式的方式都傳送。 順序如下所示：

1. 您C++Native Client ODBC 應用程式會啟動交易，藉由呼叫[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)，以自動認可模式關閉。

2. 應用程式會更新 SQL 伺服器 X 上的一些資料，在電腦 a。

3. 應用程式會更新電腦 b 上的 SQL 伺服器 Y 上資料
    - 如果在 SQL Server 的 y 軸上的更新失敗，會回復所有未認可的更新，這兩個 SQL Server 執行個體。

4. 最後，應用程式藉由呼叫結束交易[SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md)，使用 SQL_COMMIT 或 SQL_ROLLBACK 選項。

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

_(1)_ 可以叫用 MSDTC，而不需要 ODBC。 在此情況下，MSDTC 會變成交易管理員，而應用程式不會再使用**SQLEndTran**。

### <a name="only-one-distributed-transaction"></a>只能有一個分散式的交易

假設您C++Native Client ODBC 應用程式登錄在分散式交易。 接下來應用程式會在第二個分散式交易中登記。 在此情況下， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會保留原始的分散式的交易中，並在新的分散式交易中登記。

如需詳細資訊，請參閱 < [DTC 程式設計人員參考](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))。

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#在雲端中的 SQL database 的替代方案

Azure SQL Database 或 Azure SQL 資料倉儲不支援 MSDTC。

不過，分散式的交易可以建立 SQL database 讓您C#程式使用.NET 類別[System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope)。

### <a name="other-programming-languages"></a>其他程式設計語言

下列其他程式設計語言與 SQL Database 服務的分散式交易可能會提供任何支援：

- 原生C++使用 ODBC 驅動程式
- 使用 TRANSACT-SQL 的連結的伺服器
- JDBC 驅動程式

## <a name="see-also"></a>另請參閱

[執行交易 (ODBC)](performing-transactions-in-odbc.md)
