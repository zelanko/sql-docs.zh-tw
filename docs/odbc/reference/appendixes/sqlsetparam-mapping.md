---
title: "SQLSetParam 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43f15984f487dec8e77fd429f823c083c6c08a5b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 對應
**SQLSetParam**最上層的對應會繼續**SQLBindParameter**如 ODBC 2 所示。*x*。 即使在概念上類似於**SQLBindParam**，驅動程式管理員未對應**SQLSetParam**至**SQLBindParam**。 這是因為某些現有的 ODBC 2。*x*驅動程式使用的特殊值*Columnsize* (SQL_SETPARAM_VALUE_MAX)，則會對應時，驅動程式管理員會產生**SQLSetParam**最上層的**SQLBindParameter**判斷呼叫 1 時。*x* ODBC 應用程式。  
  
 呼叫  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 將會產生下列：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
