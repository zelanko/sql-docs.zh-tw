---
description: 類型識別碼
title: 類型識別碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ed41716cd351631578d01027663aa9e0f028c7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487441"
---
# <a name="type-identifiers"></a>類型識別碼
為了描述 SQL 和 C 資料類型，ODBC 會定義兩組 *類型識別碼*。 型別識別碼描述 SQL 資料行或 C 緩衝區的型別。 它是 **#define** 值，通常會以函式引數形式傳遞或在中繼資料中傳回。  
  
 例如，下列對 **SQLBindParameter** 的呼叫會將類型 SQL_DATE_STRUCT 的變數系結至 SQL 語句中的 DATE 參數。 C 類型識別碼 SQL_C_TYPE_DATE 指定 *日期* 變數的類型，而 SQL 類型識別碼 SQL_TYPE_DATE 指定動態參數的類型。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
