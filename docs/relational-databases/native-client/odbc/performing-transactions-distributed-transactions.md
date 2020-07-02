---
title: 建立分散式交易 |Microsoft Docs
description: 應用程式可以使用 MSDTC，在多個 SQL Server 實例之間擴充或散發交易。 .NET 類別也可以散發交易。
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9af1f5a9431c9ccfd5b51b26f9574a3960898102
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787797"
---
# <a name="create-a-distributed-transaction"></a>建立分散式交易

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


您可以用不同的方式為不同的 Microsoft SQL 系統建立分散式交易。

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 驅動程式會呼叫 MSDTC 進行內部部署 SQL Server

Microsoft 分散式交易協調器（MSDTC）可讓應用程式在兩個或多個實例之間擴充或_散發_交易 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 即使兩個實例裝載于不同的電腦上，分散式交易仍然可以運作。

MSDTC 是針對內部部署 Microsoft SQL Server 進行安裝，但不適用於 Microsoft 的 Azure SQL Database 雲端服務。

當您的 c + + 程式管理分散式交易時，SQL Server Native Client driver for 開放式資料庫連接（ODBC）會呼叫 MSDTC。 Native Client ODBC 驅動程式具有符合開放式群組分散式交易處理（DTP） XA 標準的交易管理員。 MSDTC 需要此合規性。 一般來說，所有交易管理命令都是透過這個 Native Client ODBC 驅動程式來傳送。 順序如下：

1. 您的 c + + Native Client ODBC 應用程式會藉由呼叫[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)（已關閉自動認可模式）來啟動交易。

2. 應用程式會更新電腦 A 上 SQL Server X 上的某些資料。

3. 應用程式會更新電腦 B 上 SQL Server Y 上的某些資料。
    - 如果 SQL Server Y 上的更新失敗，則兩個 SQL Server 實例上所有未認可的更新都會復原。

4. 最後，應用程式會藉由使用 SQL_COMMIT 或 SQL_ROLLBACK 選項來呼叫[SQLEndTran _（1）_](../../../relational-databases/native-client-odbc-api/sqlendtran.md)來結束交易。

_（1）_ MSDTC 不需要 ODBC 就可以叫用。 在這種情況下，MSDTC 會變成交易管理員，而應用程式不會再使用**SQLEndTran**。

### <a name="only-one-distributed-transaction"></a>只有一個分散式交易

假設您的 c + + Native Client ODBC 應用程式已登記在分散式交易中。 接下來，應用程式會在第二個分散式交易中登記。 在此情況下， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會離開原始的分散式交易，並在新的分散式交易中登記。

如需詳細資訊，請參閱 DTC 程式設計[人員參考](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))。

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>雲端中 SQL Database 的 c # 替代方案

Azure SQL Database 或 Azure SQL 資料倉儲都不支援 MSDTC。

不過，您可以藉由讓 c # 程式使用[.net 類別的](/dotnet/api/system.transactions.transactionscope)node.js，為 SQL Database 建立分散式交易。

### <a name="other-programming-languages"></a>其他程式設計語言

下列其他程式設計語言可能無法使用 SQL Database 服務來提供對分散式交易的任何支援：

- 使用 ODBC 驅動程式的原生 c + +
- 使用 Transact-sql 的連結伺服器
- JDBC 驅動程式

## <a name="see-also"></a>另請參閱

[執行交易 (ODBC)](performing-transactions-in-odbc.md)
