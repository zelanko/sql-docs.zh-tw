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
ms.openlocfilehash: c6682ae98f2da64f6936049bee96fe2fff2a84db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057064"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 函式
在 SQL-92 中定義的**CAST**函數相當於 ODBC 中定義的**CONVERT**函數。 對應函數的語法如下所示：  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92**轉換**函數會規定哪些資料類型可以轉換成其他資料類型。 （如需詳細資訊，請參閱 SQL-92 規格）。在 FIPS 過渡層級支援**CAST**函數。  
  
 應用程式可以判斷**CAST**函數的支援，如下所示：  
  
1.  使用 SQL_SQL_CONFORMANCE 資訊類型來呼叫**SQLGetInfo** 。 如果資訊類型的傳回值是 SQL_SC_FIPS127_2_TRANSITIONAL、SQL_SC_SQL92_INTERMEDIATE 或 SQL_SC_SQL92_FULL，則支援**CAST**函數。  
  
2.  如果 SQL_SQL_CONFORMANCE 資訊類型的傳回值 SQL_SC_ENTRY_LEVEL 或0，請使用 SQL_SQL92_VALUE_EXPRESSIONS 資訊類型來呼叫**SQLGetInfo** 。 如果已設定 SQL_SVE_CAST 位，則支援**CAST**函數。
