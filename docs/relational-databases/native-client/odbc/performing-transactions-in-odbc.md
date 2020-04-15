---
title: ODBC 中的交易 |微軟文件
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
ms.openlocfilehash: 093eae04962409b5ac426713aedc74aa1bd0703b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303646"
---
# <a name="performing-transactions-in-odbc"></a>在 ODBC 中執行交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 中的交易會在連接層級進行管理。 當應用程式完成交易時，它會認可或回復透過該連接之所有陳述式控制代碼完成的所有工作。 要提交或回滾事務,應用程式應呼叫[SQLEndTran 而不是](../../../relational-databases/native-client-odbc-api/sqlendtran.md)提交 COMMIT 或 ROLLBACK 語句。  
  
 應用程式呼叫[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)在管理事務的兩種 ODBC 模式之間切換:  
  
-   自動認可模式  
  
     每個陳述式都會在成功完成時自動認可。 當您在自動認可模式下執行時，不需要其他任何交易管理函數。  
  
-   手動認可模式  
  
     所有執行的語句都包含在同一事務中,直到通過調用**SQLEndTran**專門停止為止。  
  
 自動認可模式是 ODBC 的預設交易模式。 建立連接時,它處於自動提交模式,直到調用**SQLSetConnectAttr**通過關閉自動提交模式來切換到手動提交模式。 當應用程式關閉自動認可時，傳送到資料庫的下一個陳述式會啟動交易。 然後,事務將保持有效,直到應用程式使用SQL_COMMIT或SQL_ROLLBACK選項調用**SQLEndTran。** **SQLEndTran**啟動下一個事務後發送到資料庫的命令。  
  
 如果應用程式從手動認可模式切換到自動認可模式，驅動程式會認可目前在連接上開啟的所有交易。  
  
 ODBC 應用程式不應使用 Transact-SQL 交易陳述式 (例如，BEGIN TRANSACTION、COMMIT TRANSACTION 或 ROLLBACK TRANSACTION)，因為這可能會在驅動程式上造成未定的行為。 ODBC 應用程式應在自動提交模式下運行,不使用任何事務管理函數或語句,或在手動提交模式下運行,並使用 ODBC **SQLEndTran**函數提交或回滾事務。  
  
## <a name="see-also"></a>另請參閱  
 [執行交易&#40;ODBC&#41;](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
