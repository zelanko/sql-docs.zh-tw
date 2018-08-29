---
title: 呼叫預存程序 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82845d2faac407385cf3ec8036fd6b63e5457b3c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085172"
---
# <a name="running-stored-procedures---call-stored-procedures"></a>執行預存程序 - 呼叫預存程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 驅動程式支援將預存程序當做遠端預存程序執行。 將預存程序當做遠端預存程序執行可讓驅動程式和伺服器最佳化執行程序的效能。  
  
  當 SQL 陳述式使用 ODBC CALL 逸出子句呼叫預存程序時，Microsoft® SQL Server™ 驅動程式會使用遠端預存程序呼叫 (RPC) 機制將程序傳送到 SQL Server。 RPC 要求會略過 SQL Server 中大部分的陳述式剖析和參數處理，也比使用 Transact-SQL EXECUTE 陳述式來得快。  
  
 示範這項功能的範例應用程式，請參閱[程序傳回碼和輸出參數&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md)。  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>將程序當做 RPC 執行  
  
1.  建構使用 ODBC CALL 逸出序列的 SQL 陳述式。 此陳述式會針對每個輸入、輸入/輸出和輸出參數，以及程序傳回值 (若有) 使用參數標記：  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  呼叫[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)每個輸入、 輸入/輸出和輸出參數，以及程序傳回值 （如果有的話）。  
  
3.  執行陳述式搭配[SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)。  
  
> [!NOTE]  
>  如果應用程式使用 Transact-SQL EXECUTE 語法 (相對於 ODBC CALL 逸出序列) 來提交程序，則 SQL Server ODBC 驅動程式會將程序呼叫當做 SQL 陳述式 (而不是 RPC) 傳遞到 SQL Server。 此外，如果使用 Transact-SQL EXECUTE 陳述式，則不會傳回輸出參數。  
  
## <a name="see-also"></a>另請參閱  
  [批次的預存程序呼叫](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [呼叫預存程序](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [程序](../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
  
