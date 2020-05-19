---
title: 批次處理預存程序呼叫 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ce14de191cb8b57496cf2de87d241810e32624ec
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709877"
---
# <a name="batching-stored-procedure-calls"></a>批次預存程序呼叫
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式會在適當時，自動將預存程序呼叫分批批次處理至伺服器。 只有在使用 ODBC CALL 逸出序列時，驅動程式才會執行此動作；它不會針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 陳述式執行此動作。 批次預存程序呼叫可以減少往返伺服器的次數，並明顯增加效能。  
  
 當您執行包含多個 ODBC CALL 逸出序列的批次時，驅動程式會批次處理伺服器的程序呼叫。 搭配 ODBC CALL 逸出序列使用繫結的參數陣列時，它也會批次處理程序呼叫。 例如，如果您使用資料列取向或資料行取向的參數系結，將具有五個元素的陣列系結至 ODBC CALL SQL 語句的參數，則在呼叫**SQLExecute**或**SQLExecDirect**時，驅動程式會將具有五個程序呼叫的單一批次傳送至伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](running-stored-procedures.md)  
  
  
