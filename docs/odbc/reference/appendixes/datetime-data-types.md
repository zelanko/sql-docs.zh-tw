---
title: Datetime 資料類型 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20d53f9d19845cb55af304ce08a321bfc07d44b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="datetime-data-types"></a>Datetime 資料類型
在 ODBC 3 *.x*、 識別項的日期、 時間和時間戳記 SQL 資料類型已從 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP (的執行個體 **#define** 9、 10 和 11 的標頭檔中) 以 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (的執行個體 **#define** 92 和 93 91 的標頭檔中)，分別。 識別碼已從 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，和 SQL_C_TYPE_TIMESTAMP，分別對應的 C 類型和執行個體 **#define**已變更據以。  
  
 資料行大小和小數位數傳回 SQL datetime 資料類型，在 ODBC 3 *.x*都是相同的有效位數和小數位數為其傳回 ODBC 2。*x*。 這些值是不同的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述項欄位中的值。 (如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。)  
  
 這些變更會影響**SQLDescribeCol**， **SQLDescribeParam**，和**SQLColAttributes**;**SQLBindCol**， **SQLBindParameter**，和**SQLGetData**; 和**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLStatistics**，和**SQLSpecialColumns**。  
  
 ODBC 3 *.x*驅動程式處理之前的段落根據 SQL_ATTR_ODBC_VERSION 環境屬性的設定中所列的函式呼叫。 如**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLSpecialColumns**，和**SQLStatistics**，如果 SQL_ATTR_ODBC_VERSION 設定為 sql_ov_odbc3 時，傳回的函式 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP DATA_TYPE 欄位中。 COLUMN_SIZE 資料行 (在所傳回的結果集**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**，和**SQLSpecialColumns**)包含近似數值類型的二進位有效位數。 NUM_PREC_RADIX 資料行 (在所傳回的結果集**SQLColumns**， **SQLGetTypeInfo**，和**SQLProcedureColumns**) 包含的值為 2。 如果 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC2，則函式傳回的 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP DATA_TYPE 欄位中，COLUMN_SIZE 資料行包含的小數有效位數近似數值類型，與 NUM_PREC_RADIX 資料行包含值為 10。  
  
 所有資料類型的呼叫中的都要求時**SQLGetTypeInfo**，函式所傳回的結果集將包含 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，定義在 ODBC 3 *.x*，SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP ODBC 2 中所定義。*x*。  
  
 因為如何 ODBC 3 *.x*驅動程式管理員會執行對應的日期、 時間和時間戳記資料類型，ODBC 3 *.x*驅動程式只需要辨識 **#defines** 91 的 92，，和中輸入的日期、 時間和時間戳記 C 資料類型的 93 *TargetType*引數的**SQLBindCol**和**SQLGetData**或*ValueType*引數的**SQLBindParameter**，而且只需要辨識 **#defines**的 91，92 和 93 日期、 時間、 與中輸入的時間戳記SQL資料類型*ParameterType*引數的**SQLBindParameter**或*DataType*引數的**SQLGetTypeInfo**。 如需詳細資訊，請參閱[Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
