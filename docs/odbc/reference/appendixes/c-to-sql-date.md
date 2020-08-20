---
description: C 到 SQL：日期
title: C 到 SQL：日期 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f9d8bed4b16ee1c63134cdb9e1ae0b8303b0deb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500001"
---
# <a name="c-to-sql-date"></a>C 到 SQL：日期
日期 ODBC C 資料類型的識別碼為：  
  
 SQL_C_TYPE_DATE  
  
 下表顯示可轉換日期 C 資料的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行位元組長度 >= 10<br /><br /> 資料行位元組長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行字元長度 >= 10<br /><br /> 資料行字元長度 < 10<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|資料值為有效的日期<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值為有效的日期 [a]<br /><br /> 資料值不是有效的日期|n/a<br /><br /> 22007|  
  
 [a] 時間戳記的時間部分設為零。  
  
 如需 SQL_C_TYPE_DATE 結構中有效值的相關資訊，請參閱本附錄先前的 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 當日期 C 資料轉換成字元 SQL 資料時，產生的字元資料會採用 "*yyyy* - *mm* - *dd*" 格式。  
  
 從日期 C 資料類型轉換資料時，驅動程式會忽略長度/指標值，並假設資料緩衝區的大小是日期 C 資料類型的大小。 長度/指標值會傳遞至**SQLPutData**中的*StrLen_or_Ind*引數，以及在**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的緩衝區。 資料緩衝區會以**SQLPutData**中的*DataPtr*引數和**SQLBindParameter**中的*ParameterValuePtr*引數來指定。
