---
title: "SQL 92 CAST 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0e62a85a53da521710ed4cc61d0260e2182fb26
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sql-92-cast-function"></a>SQL 92 CAST 函數
**轉換**以 sql-92 定義的函數即相當於**轉換**ODBC 中定義的函式。 對等函式的語法如下所示：  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL 92**轉換**函式所要求的資料類型可以轉換成其他資料類型。 （如需詳細資訊，請參閱 sql-92 規格）。**轉換**FIPS 過渡期的層級支援函式。  
  
 應用程式可以決定支援的**轉換**函式，如下所示：  
  
1.  呼叫**SQLGetInfo** SQL_SQL_CONFORMANCE 資訊類型。 如果資訊類型的傳回值是 SQL_SC_FIPS127_2_TRANSITIONAL、 SQL_SC_SQL92_INTERMEDIATE 或 SQL_SC_SQL92_FULL，**轉換**支援函式。  
  
2.  如果 SQL_SC_ENTRY_LEVEL 或 0 SQL_SQL_CONFORMANCE 資訊類型的傳回值，呼叫**SQLGetInfo** SQL_SQL92_VALUE_EXPRESSIONS 資訊類型。 如果設定 SQL_SVE_CAST 位元，**轉換**支援函式。
