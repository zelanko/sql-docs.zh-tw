---
title: Datetime 資料類型 |Microsoft Docs
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
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cb92afa9467717b8a589ddbcaee4ab8a5a529f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130085"
---
# <a name="datetime-data-types"></a>日期時間資料類型
在 ODBC *3.x 中，* 日期、時間和時間戳記 SQL 資料類型的識別碼已從 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP （包含9、10和11的標頭檔中 **#define**的實例）變更為 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP （分別為91、92和93的標頭檔中 **#define**的實例）。 對應的 C 類型識別碼已從 SQL_C_DATE、SQL_C_TIME 和 SQL_C_TIMESTAMP 變更為分別 SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和 SQL_C_TYPE_TIMESTAMP，而 **#define**的實例也已變更。  
  
 ODBC 3.x 中 SQL datetime 資料類型所傳回的資料行大小和十進位數，與*在 odbc 2.x*中為其傳回的有效位數和小數位數*相同。* 這些值與 [SQL_DESC_PRECISION] 和 [SQL_DESC_SCALE 描述項] 欄位中的值不同。 （如需詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)）。  
  
 這些變更會影響**SQLDescribeCol**、 **SQLDescribeParam**和**SQLColAttributes**;**SQLBindCol**、 **SQLBindParameter**和**SQLGetData**;和**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLStatistics**和**SQLSpecialColumns**。  
  
 *ODBC 3.x*驅動程式會根據 SQL_ATTR_ODBC_VERSION 環境屬性的設定，處理上一個段落中所列的函式呼叫。 若為**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLSpecialColumns**和**SQLStatistics**，如果 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC3，則函式會在 SQL_TYPE_TIMESTAMP 欄位中傳回 SQL_TYPE_DATE、SQL_TYPE_TIME 和 DATA_TYPE。 COLUMN_SIZE 資料行（在**SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**和**SQLSpecialColumns**所傳回的結果集中）包含近似數數值型別的二進位有效位數。 NUM_PREC_RADIX 的資料行（在**SQLColumns**、 **SQLGetTypeInfo**和**SQLProcedureColumns**所傳回的結果集中）包含2的值。 如果 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC2，則函數會在 SQL_TIMESTAMP 欄位中傳回 SQL_DATE、SQL_TIME 和 DATA_TYPE、COLUMN_SIZE 資料行包含近似數數值型別的十進位有效位數，以及 NUM_PREC_RADIX 資料行包含10的值。  
  
 在**SQLGetTypeInfo**的呼叫中要求所有資料類型時，函式所傳回的結果集將包含 odbc 3.x 中所定義的 SQL_TYPE_DATE、SQL_TYPE_TIME 和*SQL_TYPE_TIMESTAMP，以及*odbc 2.x 中所定義的 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP。 **  
  
 因為*ODBC 3.X*驅動程式管理員如何執行日期的對應，時間和時間戳記資料類型 *，ODBC 3.x*驅動程式只需要針對**SQLBindCol**和**SQLGetData**的*TargetType*引數或**SQLBindParameter**的*ValueType*引數所輸入的日期、時間和時間戳記 C 資料類型，辨識91、92和 93 **#defines** ，而且只需要辨識91、92和93的 **#defines** ，以取得在中輸入的日期、時間和時間戳記 SQL 資料類型**SQLBindParameter**的*ParameterType*引數或**SQLGetTypeInfo**的*DataType*引數。 如需詳細資訊，請參閱[Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
