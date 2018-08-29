---
title: ODBC 中的交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ba7af1fa77fc310860a3f0fdca84c9b203549c7b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058927"
---
# <a name="performing-transactions-in-odbc"></a>在 ODBC 中執行交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 中的交易會在連接層級進行管理。 當應用程式完成交易時，它會認可或回復透過該連接之所有陳述式控制代碼完成的所有工作。 若要認可或回復交易，應用程式應該呼叫[SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md)而非提交 COMMIT 或 ROLLBACK 陳述式。  
  
 應用程式呼叫[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)管理交易的兩個 ODBC 模式之間切換：  
  
-   自動認可模式  
  
     每個陳述式都會在成功完成時自動認可。 當您在自動認可模式下執行時，不需要其他任何交易管理函數。  
  
-   手動認可模式  
  
     所有執行的陳述式包含相同交易中，直到它特別會停止藉由呼叫**SQLEndTran**。  
  
 自動認可模式是 ODBC 的預設交易模式。 建立連接時，它處於自動認可模式，直到**SQLSetConnectAttr**呼叫以自動認可模式設定的手動認可模式關閉。 當應用程式關閉自動認可時，傳送到資料庫的下一個陳述式會啟動交易。 接著，交易會維持作用中直到應用程式會呼叫**SQLEndTran** SQL_COMMIT 或 SQL_ROLLBACK 選項。 命令傳送至資料庫後**SQLEndTran**會啟動下一個交易。  
  
 如果應用程式從手動認可模式切換到自動認可模式，驅動程式會認可目前在連接上開啟的所有交易。  
  
 ODBC 應用程式不應使用 Transact-SQL 交易陳述式 (例如，BEGIN TRANSACTION、COMMIT TRANSACTION 或 ROLLBACK TRANSACTION)，因為這可能會在驅動程式上造成未定的行為。 ODBC 應用程式應該在自動認可模式中執行和不使用任何交易管理函數或陳述式，或在手動認可模式下執行並使用 ODBC **SQLEndTran**函式，來認可或回復交易。  
  
## <a name="see-also"></a>另請參閱  
 [執行交易&#40;ODBC&#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
