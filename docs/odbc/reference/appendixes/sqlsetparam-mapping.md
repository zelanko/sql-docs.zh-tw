---
description: SQLSetParam 對應
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
ms.openlocfilehash: e2c16f942920b5fefff664cc647f4edfc9ab6d13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339294"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 對應
**SQLSetParam** 會繼續對應到 **SQLBindParameter** 上的，如 ODBC 2 所示。*x*。 雖然在概念上類似于 **SQLBindParam**，但驅動程式管理員不會將 **SQLSetParam** 對應到 **SQLBindParam**。 這是因為某些現有的 ODBC 2。*x* 驅動程式會使用 *BufferLength* (的特殊值 SQL_SETPARAM_VALUE_MAX) 驅動程式管理員在將 **SQLSetParam** 對應到 **SQLBindParameter** 上時所產生的值，以判斷由1呼叫它的時間。*x* ODBC 應用程式。  
  
 呼叫  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 將會產生下列結果：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
