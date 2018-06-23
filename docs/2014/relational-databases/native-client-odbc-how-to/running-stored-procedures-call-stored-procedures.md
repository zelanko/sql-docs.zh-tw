---
title: 呼叫預存程序 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0846567d803eadf4364159fc01fdb8a7853e8a4f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035911"
---
# <a name="call-stored-procedures-odbc"></a>呼叫預存程序 (ODBC)
  當 SQL 陳述式使用 ODBC CALL 逸出子句呼叫預存程序時，Microsoft® SQL Server™ 驅動程式會使用遠端預存程序呼叫 (RPC) 機制將程序傳送到 SQL Server。 RPC 要求會略過 SQL Server 中大部分的陳述式剖析和參數處理，也比使用 Transact-SQL EXECUTE 陳述式來得快。  
  
 範例應用程式，示範這項功能，請參閱[處理傳回碼和輸出參數&#40;ODBC&#41;](running-stored-procedures-process-return-codes-and-output-parameters.md)。  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>將程序當做 RPC 執行  
  
1.  建構使用 ODBC CALL 逸出序列的 SQL 陳述式。 此陳述式會針對每個輸入、輸入/輸出和輸出參數，以及程序傳回值 (若有) 使用參數標記：  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  呼叫[SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md)針對每個輸入、 輸入/輸出和輸出參數，和程序傳回值 （如果有的話）。  
  
3.  執行陳述式使用[SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)。  
  
> [!NOTE]  
>  如果應用程式使用 Transact-SQL EXECUTE 語法 (相對於 ODBC CALL 逸出序列) 來提交程序，則 SQL Server ODBC 驅動程式會將程序呼叫當做 SQL 陳述式 (而不是 RPC) 傳遞到 SQL Server。 此外，如果使用 Transact-SQL EXECUTE 陳述式，則不會傳回輸出參數。  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序的使用說明主題&#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [批次的預存程序呼叫](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [執行預存程序](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [呼叫預存程序](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [程序](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  