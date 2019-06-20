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
manager: craigg
ms.openlocfilehash: 4d546fff544c616d4f2750dba76c4b8e68d21aab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241008"
---
# <a name="datetime-data-types"></a>日期時間資料類型
在 ODBC 3 *.x*識別碼的日期、 時間和時間戳記 SQL 資料類型已從 SQL_DATE、 SQL_TIME、 和 SQL_TIMESTAMP (的執行個體 **#define** 9、 10 和 11 的標頭檔中) 至 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (的執行個體 **#define** 91、 92，和 93 標頭檔)，分別。 識別碼已從 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，和 SQL_C_TYPE_TIMESTAMP，分別對應的 C 類型和執行個體 **#define**已變更據此。  
  
 在 ODBC 3 SQL datetime 資料類型傳回的資料行大小和小數位數 *.x*是相同的有效位數和小數位數為其傳回的 ODBC 2。*x*。 這些值是中的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述項欄位的值不同。 (如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料型別。）  
  
 這些變更會影響**SQLDescribeCol**， **SQLDescribeParam**，並**SQLColAttributes**;**SQLBindCol**， **SQLBindParameter**，並**SQLGetData**; 以及**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLStatistics**，和**SQLSpecialColumns**。  
  
 ODBC 3 *.x*驅動程式處理之前的段落，根據 SQL_ATTR_ODBC_VERSION 環境屬性的設定中所列的函式呼叫。 針對**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**， **SQLSpecialColumns**，和**SQLStatistics**、 如果 SQL_ATTR_ODBC_VERSION 設定為 sql_ov_odbc3 時，傳回的函式 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP DATA_TYPE 欄位中。 COLUMN_SIZE 資料行 (在所傳回的結果集中**SQLColumns**， **SQLGetTypeInfo**， **SQLProcedureColumns**，和**SQLSpecialColumns**)包含二進位整數位數為近似的數值類型。 NUM_PREC_RADIX 資料行 (在所傳回的結果集中**SQLColumns**， **SQLGetTypeInfo**，並**SQLProcedureColumns**) 包含的值為 2。 如果 SQL_ATTR_ODBC_VERSION 設 SQL_OV_ODBC2，則函式傳回的 SQL_DATE、 SQL_TIME、 和 SQL_TIMESTAMP DATA_TYPE 欄位中，COLUMN_SIZE 資料行包含近似的數值類型，與 NUM_PREC_RADIX 資料行的小數有效位數包含值為 10。  
  
 所有的資料類型的呼叫中的要求時**SQLGetTypeInfo**，函式所傳回的結果集將包含 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，定義在 ODBC 3 *.x*，SQL_DATE、 SQL_TIME、 和 SQL_TIMESTAMP ODBC 2 中所定義。*x*。  
  
 造成 ODBC 3 *.x*驅動程式管理員會執行的日期、 時間和時間戳記資料類型對應，ODBC 3 *.x*驅動程式只需要辨識 **#defines**的 91、 92，和中輸入的日期、 時間和時間戳記 C 資料類型的 93 *TargetType*的引數**SQLBindCol**並**SQLGetData**或*ValueType*引數**SQLBindParameter**，而且只需要辨識 **#defines**的 91、 92 和 93 日期、 時間，但時間戳記 SQL 資料類型輸入*ParameterType*引數**SQLBindParameter**或*DataType*引數**SQLGetTypeInfo**。 如需詳細資訊，請參閱 <<c0> [ 日期時間資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
