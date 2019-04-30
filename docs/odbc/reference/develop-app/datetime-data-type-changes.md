---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5a87a1cbfbdff5eb428e73d74cdd1199955d673
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267700"
---
# <a name="datetime-data-type-changes"></a>Datetime 資料類型變更
在 ODBC 3。*x*識別碼的日期、 時間和時間戳記 SQL 資料類型已從 SQL_DATE、 SQL_TIME、 和 SQL_TIMESTAMP (的執行個體 **#define** 9、 10 和 11 的標頭檔中) 至 SQL_TYPE_DATE，SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (的執行個體 **#define** 91、 92，和 93 標頭檔)，分別。 對應的 C 類型識別項已從 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，和 SQL_C_TYPE_TIMESTAMP，分別。  
  
 傳回在 ODBC 3 SQL datetime 資料類型的小數位數及資料行大小。*x*是相同的有效位數和小數位數為其傳回的 ODBC 2。*x*。 這些值是中的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述項欄位的值不同。 (如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。)  
  
 這些變更會影響**SQLDescribeCol**， **SQLDescribeParam**，並**SQLColAttribute**;**SQLBindCol**， **SQLBindParameter**，並**SQLGetData**; 以及**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLStatistics**，和**SQLSpecialColumns**。  
  
 下表顯示如何 ODBC 3 *.x*驅動程式管理員會執行的日期、 時間和時間戳記 C 資料類型對應中輸入*TargetType*引數的**SQLBindCol**並**SQLGetData**或是在*ValueType*引數**SQLBindParameter**。  
  
|資料類型<br /><br /> 輸入的程式碼|2.*x*應用程式<br /><br /> 2.*x*驅動程式|2.*x*應用程式<br /><br /> 3.*x*驅動程式|3.*x*應用程式<br /><br /> 2.*x*驅動程式|3.*x*應用程式<br /><br /> 3.*x*驅動程式|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|沒有對應|SQL_C_TYPE_DATE (91)|沒有對應 [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|錯誤 （DM)|錯誤 （DM)|SQL_C_DATE (9)|沒有對應 [2]|  
|SQL_C_TIME (10)|沒有對應|SQL_C_TYPE_TIME (92)|沒有對應 [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|錯誤 （DM)|錯誤 （DM)|SQL_C_TIME (10)|沒有對應 [2]|  
|SQL_C_TIMESTAMP (11)|沒有對應|SQL_C_TYPE_TIMESTAMP (93)|沒有對應 [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|錯誤 （DM)|錯誤 （DM)|SQL_C_TIMESTAMP (11)|沒有對應 [2]|  
  
 [1] 的 this，ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式可以使用目錄函數所傳回之結果集內所傳回的日期、 時間戳記碼。  
  
 [2] 的 this，ODBC 3。*x*應用程式使用 ODBC 3。*x*驅動程式可以使用目錄函數所傳回之結果集內所傳回的日期、 時間戳記碼。  
  
 下表顯示如何 ODBC 3 *.x*驅動程式管理員會執行的日期、 時間和時間戳記 SQL 資料類型對應中輸入*ParameterType*引數**SQLBindParameter**或是在*DataType*引數**SQLGetTypeInfo**。  
  
|資料類型<br /><br /> 輸入的程式碼|2.*x*應用程式<br /><br /> 2.*x*驅動程式|2.*x*應用程式<br /><br /> 3.*x*驅動程式|3.*x*應用程式<br /><br /> 2.*x*驅動程式|3.*x*應用程式<br /><br /> 3.*x*驅動程式|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|沒有對應|SQL_TYPE_DATE (91)|沒有對應 [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|錯誤 （DM)|錯誤 （DM)|SQL_DATE (9)|沒有對應 [2]|  
|SQL_TIME (10)|沒有對應|SQL_TYPE_TIME (92)|沒有對應 [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|錯誤 （DM)|錯誤 （DM)|SQL_TIME (10)|沒有對應 [2]|  
|SQL_TIMESTAMP (11)|沒有對應|SQL_TYPE_TIMESTAMP (93)|沒有對應 [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|錯誤 （DM)|錯誤 （DM)|SQL_TIMESTAMP (11)|沒有對應 [2]|  
  
 [1] 的 this，ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式可以使用目錄函數所傳回之結果集內所傳回的日期、 時間戳記碼。  
  
 [2] 的 this，ODBC 3。*x*應用程式使用 ODBC 3。*x*驅動程式可以使用目錄函數所傳回之結果集內所傳回的日期、 時間戳記碼。
