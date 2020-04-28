---
title: SQLSetParam 對應 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300528"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 對應
**SQLSetParam**會繼續在**SQLBindParameter**之上對應，如同 ODBC 2 中的一樣。*x*。 雖然它在概念上類似于**SQLBindParam**，但驅動程式管理員並不會將**SQLSetParam**對應至**SQLBindParam**。 這是因為某些現有的 ODBC 2。*x*驅動程式會使用*BufferLength* （SQL_SETPARAM_VALUE_MAX）的特殊值，而驅動程式管理員會在將**SQLSetParam**對應到**SQLBindParameter**上時產生它，以判斷它是由1所呼叫的時間。*x* ODBC 應用程式。  
  
 呼叫  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 會產生下列結果：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
