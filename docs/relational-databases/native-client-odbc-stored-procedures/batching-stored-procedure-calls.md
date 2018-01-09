---
title: "批次方式預存程序呼叫 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 694a2c5cc8a9445c2e592bfaba6e5887a5874e0d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="batching-stored-procedure-calls"></a>批次預存程序呼叫
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式，自動批次處理伺服器在適當時的預存程序呼叫。 只有在使用 ODBC CALL 逸出序列時，驅動程式才會執行此動作；它不會針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 陳述式執行此動作。 批次預存程序呼叫可以減少往返伺服器的次數，並明顯增加效能。  
  
 當您執行包含多個 ODBC CALL 逸出序列的批次時，驅動程式會批次處理伺服器的程序呼叫。 搭配 ODBC CALL 逸出序列使用繫結的參數陣列時，它也會批次處理程序呼叫。 例如，如果您使用其中一個資料列取向或資料行取向的參數繫結至 ODBC CALL SQL 陳述式的參數繫結具有五個元素的陣列時**SQLExecute**或**SQLExecDirect**呼叫時，驅動程式會傳送到伺服器的五個程序呼叫的單一批次。  
  
## <a name="see-also"></a>請參閱  
 [執行預存程序](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
