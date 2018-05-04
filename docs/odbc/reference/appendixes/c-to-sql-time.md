---
title: SQL 到 C： 時間 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac288b1b1985d106e88254a23eed2d973425c6f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-time"></a>SQL 到 C： 時間
時間 ODBC C 資料類型的識別項是：  
  
 SQL_C_TYPE_TIME  
  
 下表顯示 ODBC SQL 資料類型可能會轉換階段 C 資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行的位元組長度 > = 8<br /><br /> 資料行長度的位元組數 < 8<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行的字元長度 > = 8<br /><br /> 資料行的字元長度 < 8<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|資料值是有效的時間<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值是有效的時間 [a]<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22007|  
  
 [a] 的日期部分的時間戳記設為目前的日期和時間戳記部分設為零的小數秒數。  
  
 如需有效值 SQL_C_TYPE_TIME 結構中的資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中。  
  
 當時間 C 資料會轉換成字元的 SQL 資料時，產生的字元資料就會處於 「*hh*:*公釐*:*ss*」 格式。  
  
 驅動程式會忽略轉換資料的 C 資料類型，並假設資料緩衝區的大小是時間 C 資料類型大小的時間長度/指標值。 長度/指標值傳遞*StrLen_or_Ind*引數中的**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*引數中的**SQLPutData**和*ParameterValuePtr*引數中的**SQLBindParameter**.
