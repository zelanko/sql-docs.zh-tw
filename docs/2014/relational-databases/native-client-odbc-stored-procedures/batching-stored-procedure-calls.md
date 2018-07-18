---
title: 批次預存程序呼叫 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1a6c75c4dd4d13a5905615836d666fe33769a6a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427787"
---
# <a name="batching-stored-procedure-calls"></a>批次預存程序呼叫
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式，自動批次處理伺服器在適當的預存程序呼叫。 只有在使用 ODBC CALL 逸出序列時，驅動程式才會執行此動作；它不會針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] EXECUTE 陳述式執行此動作。 批次預存程序呼叫可以減少往返伺服器的次數，並明顯增加效能。  
  
 當您執行包含多個 ODBC CALL 逸出序列的批次時，驅動程式會批次處理伺服器的程序呼叫。 搭配 ODBC CALL 逸出序列使用繫結的參數陣列時，它也會批次處理程序呼叫。 例如，如果您使用其中一個資料列取向或資料行取向參數繫結繫結具有五個元素的陣列至 ODBC CALL SQL 陳述式的參數時**SQLExecute**或是**SQLExecDirect**呼叫時，驅動程式會傳送到伺服器的五個程序呼叫的單一批次。  
  
## <a name="see-also"></a>另請參閱  
 [執行預存程序](running-stored-procedures.md)  
  
  
