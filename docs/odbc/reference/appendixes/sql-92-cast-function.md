---
title: SQL-92 CAST 功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d2a2de710dafd4e744166c4219f4c903fd3321
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305059"
---
# <a name="sql-92-cast-function"></a>SQL-92 CAST 函式
SQL-92 中定義的**CAST**函數等效於 ODBC 中定義的**CONVERT**函數。 等效函數的語法如下:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **CAST**函數要求哪些數據類型可以轉換為哪些其他數據類型。 (有關詳細資訊,請參閱 SQL-92 規範。在 FIPS 過渡等級支援**CAST**功能。  
  
 應用程式可以確定對**CAST**函數的支援,如下所示:  
  
1.  使用SQL_SQL_CONFORMANCE資訊類型調用**SQLGetInfo。** 如果資訊類型的返回值SQL_SC_FIPS127_2_TRANSITIONAL、SQL_SC_SQL92_INTERMEDIATE 或SQL_SC_SQL92_FULL,則支援**CAST**函數。  
  
2.  如果SQL_SQL_CONFORMANCE資訊類型的返回值為 SQL_SC_ENTRY_LEVEL 或 0,請使用SQL_SQL92_VALUE_EXPRESSIONS資訊類型調用**SQLGetInfo。** 如果設置了SQL_SVE_CAST位,則支援**CAST**函數。
