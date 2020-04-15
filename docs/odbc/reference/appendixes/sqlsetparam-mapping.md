---
title: SQLSetParam 對應 ( P)微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300528"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 對應
**SQLSetParam**繼續映射到**SQLBind 參數**之上,如 ODBC 2 中一樣。*x*. . 儘管它在概念上與**SQLBindParam**類似,但驅動程式管理器不會將**SQLSetParam**映射到**SQLBindParam。** 這是因為某些現有的ODBC 2。*x*驅動程式使用驅動程式管理器在**SQLBind 參數**頂部映射**SQLSetParam**時生成的緩衝區*長度*(SQL_SETPARAM_VALUE_MAX) 的特殊值來確定何時由 1 調用它。*x* ODBC 應用。  
  
 通話  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 將導致以下結果:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
