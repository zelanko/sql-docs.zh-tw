---
title: 建立分散式事務 |微軟文件
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
ms.openlocfilehash: f21ea9b7146b2907a09688f5189d6d9ae4f3f26a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303683"
---
# <a name="create-a-distributed-transaction"></a>建立分散式事務

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


可以以不同的方式為不同的 Microsoft SQL 系統創建分散式事務。

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 驅動程式在本地呼叫 SQL Server 的 MSDTC

Microsoft 分散式事務協調器 (MSDTC) 允許應用程式跨 的兩個或多個實體延伸或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]_分發_事務 。 即使兩個實例託管在單獨的計算機上,分散式事務也能正常工作。

MSDTC 安裝在本地為Microsoft SQL伺服器,但不適用於Microsoft的Azure SQL資料庫雲端服務。

MSDTC 由打開資料庫連接 (ODBC) 的 SQL Server 本機客戶端驅動程式呼叫,當您 C++程式管理分散式事務時。 本機用戶端 ODBC 驅動程式具有符合開放組分散式事務處理 (DTP) XA 標準的事務管理器。 MSDTC 需要這種合規性。 通常,所有事務管理命令都通過此本機用戶端ODBC驅動程式發送。 順序如下：

1. C++本機用戶端 ODBC 應用程式通過調用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)啟動事務,自動提交模式處於關閉狀態。

2. 應用程式在電腦 A 上更新 SQL Server X 上的一些數據。

3. 應用程式在電腦 B 上更新 SQL Server Y 上的一些數據。
    - 如果 SQL Server Y 上的更新失敗,則回滾兩個 SQL Server 實例上未提交的所有更新。

4. 最後,應用程式通過調用[SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md)結束事務,SQL_COMMIT 或SQL_ROLLBACK選項。

_(1)_ 無需 ODBC 即可呼叫 MSDTC。 在這種情況下,MSDTC 成為事務管理員,應用程式不再使用**SQLEndTran**。

### <a name="only-one-distributed-transaction"></a>只有一個分散式事務

假設您C++本機用戶端 ODBC 應用程式已登記在分散式事務中。 接下來,應用程式將登記在第二個分散式事務中。 在這種情況下,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式將離開原始分散式事務,並登記在新的分散式事務中。

有關詳細資訊,請參閱[DTC 程式設計師的參考](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))。

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>雲中 SQL 資料庫的 C# 替代方案

Azure SQL 資料庫或 Azure SQL 資料倉儲不支援 MSDTC。

但是,可以通過讓 C# 程式使用 .NET 類[系統,](/dotnet/api/system.transactions.transactionscope)為 SQL 資料庫創建分散式事務。

### <a name="other-programming-languages"></a>其他程式設計語言

以下其他程式設計語言可能無法為 SQL 資料庫服務的分散式事務提供任何支援:

- 使用 ODBC 驅動程式的本機C++
- 使用交易 SQL 連結伺服器
- JDBC 驅動程式

## <a name="see-also"></a>另請參閱

[執行交易 (ODBC)](performing-transactions-in-odbc.md)
