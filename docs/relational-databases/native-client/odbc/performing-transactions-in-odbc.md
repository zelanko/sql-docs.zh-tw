---
title: ODBC 中的交易 |Microsoft Docs
description: ODBC 會在連接層級管理交易、認可或回復所有已完成的工作，無論是在自動認可或手動認可模式下。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e37533e1c57ccf55dfe8bb7b5cbc5aa3da60dd3f
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890790"
---
# <a name="performing-transactions-in-odbc"></a>在 ODBC 中執行交易
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC 中的交易會在連接層級進行管理。 當應用程式完成交易時，它會認可或回復透過該連接之所有陳述式控制代碼完成的所有工作。 若要認可或回復交易，應用程式應該呼叫 [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) ，而不是提交 COMMIT 或 ROLLBACK 語句。  
  
 應用程式會呼叫 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) ，在兩種管理交易的 ODBC 模式之間切換：  
  
-   自動認可模式  
  
     每個陳述式都會在成功完成時自動認可。 當您在自動認可模式下執行時，不需要其他任何交易管理函數。  
  
-   手動認可模式  
  
     所有執行的語句都會包含在相同的交易中，直到透過呼叫 **SQLEndTran**來明確停止為止。  
  
 自動認可模式是 ODBC 的預設交易模式。 建立連線時，會處於自動認可模式，直到呼叫 **SQLSetConnectAttr** 來切換至手動認可模式，方法是設定 [自動認可模式]。 當應用程式關閉自動認可時，傳送到資料庫的下一個陳述式會啟動交易。 然後，交易就會持續生效，直到應用程式使用 SQL_COMMIT 或 SQL_ROLLBACK 選項來呼叫 **SQLEndTran** 為止。 **SQLEndTran**開始下一個交易時，傳送至資料庫的命令。  
  
 如果應用程式從手動認可模式切換到自動認可模式，驅動程式會認可目前在連接上開啟的所有交易。  
  
 ODBC 應用程式不應使用 Transact-SQL 交易陳述式 (例如，BEGIN TRANSACTION、COMMIT TRANSACTION 或 ROLLBACK TRANSACTION)，因為這可能會在驅動程式上造成未定的行為。 ODBC 應用程式應該在自動認可模式下執行，而不使用任何交易管理函數或語句，或是在手動認可模式下執行，並使用 ODBC **SQLEndTran** 函數來認可或回復交易。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行交易 ]()  
  
