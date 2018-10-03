---
title: SQL-92 CAST 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db5077b9df2673593b6eaec9622aafd1d2c77234
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753986"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 函式
**CAST**以 SQL-92 定義的函式相當於**轉換**在 ODBC 中定義的函式。 對等的函式的語法如下所示：  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92**轉型**函式會強制的資料類型可以轉換成的其他資料類型。 （如需詳細資訊，請參閱 SQL-92 規格）。**轉型**支援函式是 FIPS 過渡期的層級。  
  
 應用程式可以判斷支援**轉型**函式，如下所示：  
  
1.  呼叫**SQLGetInfo** SQL_SQL_CONFORMANCE 資訊類型。 SQL_SC_FIPS127_2_TRANSITIONAL、 SQL_SC_SQL92_INTERMEDIATE 或 SQL_SC_SQL92_FULL，資訊類型的傳回值是否**轉型**支援函式。  
  
2.  如果 SQL_SC_ENTRY_LEVEL 或 0 SQL_SQL_CONFORMANCE 資訊類型的傳回值，呼叫**SQLGetInfo** SQL_SQL92_VALUE_EXPRESSIONS 資訊類型。 如果設定的 SQL_SVE_CAST 位元，則**轉型**支援函式。
