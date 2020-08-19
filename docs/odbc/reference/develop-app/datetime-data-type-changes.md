---
description: Datetime 資料類型變更
title: Datetime 資料類型變更 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a36339f275ff03584a3682f9f57eeeb8445faf3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424750"
---
# <a name="datetime-data-type-changes"></a>Datetime 資料類型變更
在 ODBC *3.x 中，* 日期、時間和時間戳記 SQL 資料類型的識別碼已從 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP (變更為9、10和 11 #define 的標頭檔中 **) ** 的實例 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (，分別為91、92和 93 #define 的頭 **檔中) ** 的實例。 對應的 C 類型識別碼已從 SQL_C_DATE、SQL_C_TIME 和 SQL_C_TIMESTAMP 分別變更為 SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和 SQL_C_TYPE_TIMESTAMP。  
  
 ODBC 3.x 中 SQL datetime 資料類型所傳回的資料行大小和小數位數，*與 odbc 2.x*中為它們傳回的精確度和小數位數*相同。* 這些值與 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述項欄位中的值不同。  (如需詳細資訊，請參閱資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。 )   
  
 這些變更會影響 **SQLDescribeCol**、 **SQLDescribeParam**和 **SQLColAttribute**; **SQLBindCol**、 **SQLBindParameter**和 **SQLGetData**;以及 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLStatistics**和 **SQLSpecialColumns**。  
  
 下表*顯示 ODBC 3.X*驅動程式管理員如何執行在**SQLBindCol**和**SQLGetData**之*TargetType*引數中輸入的日期、時間和時間戳記 C 資料類型的對應，或**SQLBindParameter**的*ValueType*引數中所輸入的日期、時間和時間戳記 C 資料類型的對應。  
  
|資料類型<br /><br /> 輸入的程式碼|2.x*應用程式*到<br /><br /> 2.x*驅動程式*|2.x*應用程式*到<br /><br /> 3.x*驅動程式*|*3. x* 應用程式到<br /><br /> 2.x*驅動程式*|*3. x* 應用程式到<br /><br /> 3.x*驅動程式*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9) |無對應|SQL_C_TYPE_DATE (91) |沒有對應 [1]|SQL_C_TYPE_DATE (91) |  
|SQL_C_TYPE_DATE (91) |從 DM)  (時發生錯誤|從 DM)  (時發生錯誤|SQL_C_DATE (9) |沒有對應 [2]|  
|SQL_C_TIME (10) |無對應|SQL_C_TYPE_TIME (92) |沒有對應 [1]|SQL_C_TYPE_TIME (92) |  
|SQL_C_TYPE_TIME (92) |從 DM)  (時發生錯誤|從 DM)  (時發生錯誤|SQL_C_TIME (10) |沒有對應 [2]|  
|SQL_C_TIMESTAMP (11) |無對應|SQL_C_TYPE_TIMESTAMP (93) |沒有對應 [1]|SQL_C_TYPE_TIMESTAMP (93) |  
|SQL_C_TYPE_TIMESTAMP (93) |從 DM)  (時發生錯誤|從 DM)  (時發生錯誤|SQL_C_TIMESTAMP (11) |沒有對應 [2]|  
  
 [1] 因此，*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*，可以使用目錄函式所傳回之結果集中傳回的日期、時間或時間戳記代碼。  
  
 [2] 因此，*使用 odbc 3.x* *驅動程式的 odbc 3.x 應用程式*，可以使用目錄函數所傳回之結果集中傳回的日期、時間或時間戳記代碼。  
  
 下表*顯示 ODBC 3.X*驅動程式管理員如何執行在**SQLBindParameter**的*ParameterType*引數或**SQLGetTypeInfo**的*DataType*引數中輸入的日期、時間和時間戳記 SQL 資料類型的對應。  
  
|資料類型<br /><br /> 輸入的程式碼|2.x*應用程式*到<br /><br /> 2.x*驅動程式*|2.x*應用程式*到<br /><br /> 3.x*驅動程式*|*3. x* 應用程式到<br /><br /> 2.x*驅動程式*|*3. x* 應用程式到<br /><br /> 3.x*驅動程式*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9) |無對應|SQL_TYPE_DATE (91)|沒有對應 [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|從 DM)  (時發生錯誤|從 DM)  (時發生錯誤|SQL_DATE (9) |沒有對應 [2]|  
|SQL_TIME (10) |無對應|SQL_TYPE_TIME (92) |沒有對應 [1]|SQL_TYPE_TIME (92) |  
|SQL_TYPE_TIME (92) |從 DM)  (時發生錯誤|從 DM)  (時發生錯誤|SQL_TIME (10) |沒有對應 [2]|  
|SQL_TIMESTAMP (11) |無對應|SQL_TYPE_TIMESTAMP (93)|沒有對應 [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|從 DM)  (時發生錯誤|從 DM)  (時發生錯誤|SQL_TIMESTAMP (11) |沒有對應 [2]|  
  
 [1] 因此，*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*，可以使用目錄函式所傳回之結果集中傳回的日期、時間或時間戳記代碼。  
  
 [2] 因此，*使用 odbc 3.x* *驅動程式的 odbc 3.x 應用程式*，可以使用目錄函數所傳回之結果集中傳回的日期、時間或時間戳記代碼。
