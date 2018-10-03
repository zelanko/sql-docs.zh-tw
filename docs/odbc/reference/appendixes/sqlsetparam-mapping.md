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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5d420bc68c4704705018a37c6459181481b1d7d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767806"
---
# <a name="sqlsetparam-mapping"></a>SQLSetParam 對應
**SQLSetParam**頂端的對應會繼續**SQLBindParameter**如 ODBC 2。*x*。 即使在概念上類似於**SQLBindParam**，則驅動程式管理員不會對應**SQLSetParam**來**SQLBindParam**。 這是因為某些現有的 ODBC 2。*x*驅動程式使用的特殊值*Columnsize* (SQL_SETPARAM_VALUE_MAX) 驅動程式管理員時，產生對應**SQLSetParam**頂端**SQLBindParameter**來判斷呼叫 1 時。*x* ODBC 應用程式。  
  
 呼叫  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 將會產生下列：  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
