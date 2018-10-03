---
title: 型別識別項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbefab0f02f3229d8b4c0a62a568634ec222290b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825166"
---
# <a name="type-identifiers"></a>類型識別碼
若要描述 SQL 和 C 資料類型，ODBC 會定義兩組*型別識別項*。 型別識別項描述 SQL 資料行或 C 的緩衝區的類型。 很 **#define**值，而為通常做為函式引數傳遞或傳回中繼資料中。  
  
 例如，下列呼叫來**SQLBindParameter**繫結至 SQL 陳述式中的日期參數的類型 SQL_DATE_STRUCT 的變數。 C 類型識別碼 SQL_C_TYPE_DATE 指定的型別*日期*變數中，以及 SQL 型別識別項 SQL_TYPE_DATE 指定動態參數的型別。  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
