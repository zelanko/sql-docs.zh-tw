---
title: 類型識別符 |微軟文件
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
ms.openlocfilehash: a274a19eaa0a2fdf98bcaa9ef42406ee8a6b6461
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306429"
---
# <a name="type-identifiers"></a>類型識別碼
為了描述 SQL 與 C 資料類型,ODBC 定義了兩組*類型識別碼*。 類型識別碼描述 SQL 列或 C 緩衝區的類型。 它是**一個#define**值,通常作為函數參數傳遞或在元數據中返回。  
  
 例如,以下對**SQLBind 參數**的調用將類型SQL_DATE_STRUCT變數綁定到 SQL 語句中的日期參數。 C 類型識別碼SQL_C_TYPE_DATE指定*Date*變數的類型,SQL 類型識別符SQL_TYPE_DATE指定動態參數的類型。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
