---
description: 日期時間資料類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a908ab61741ad46ec00a341552a15db44cd5b603
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456625"
---
# <a name="datetime-data-types"></a>日期時間資料類型
在 ODBC *3.x 中，* 日期、時間和時間戳記 SQL 資料類型的識別碼已從 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP (變更為9、10和 11 #define 的標頭檔中 **) ** 的實例 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP (，分別為91、92和 93 #define 的頭 **檔中) ** 的實例。 對應的 C 類型識別碼已從 SQL_C_DATE、SQL_C_TIME 和 SQL_C_TIMESTAMP 分別變更為 SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和 SQL_C_TYPE_TIMESTAMP，且 **#define** 的實例已據以變更。  
  
 ODBC 3.x 中 SQL datetime 資料類型所傳回的資料行大小和小數位數，*與 odbc 2.x*中為它們傳回的精確度和小數位數*相同。* 這些值與 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 描述項欄位中的值不同。  (如需詳細資訊，請參閱附錄 D：資料類型中的資料 [行大小、十進位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 。 )   
  
 這些變更會影響 **SQLDescribeCol**、 **SQLDescribeParam**和 **SQLColAttributes**; **SQLBindCol**、 **SQLBindParameter**和 **SQLGetData**;以及 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLStatistics**和 **SQLSpecialColumns**。  
  
 *ODBC 3.x*驅動程式會根據 SQL_ATTR_ODBC_VERSION 環境屬性的設定，處理上一個段落中所列的函式呼叫。 針對 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**、 **SQLSpecialColumns**和 **SQLStatistics**，如果 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC3，函數會傳回 SQL_TYPE_TIMESTAMP 欄位中 SQL_TYPE_DATE、SQL_TYPE_TIME 和 DATA_TYPE。 **SQLColumns**、 **SQLGetTypeInfo**、 **SQLProcedureColumns**和**SQLSpecialColumns**所傳回之結果集中的 COLUMN_SIZE 資料行 () 包含大約數數值型別的二進位精確度。 **SQLColumns**、 **SQLGetTypeInfo**和) **SQLProcedureColumns**所傳回之結果集中的 NUM_PREC_RADIX 資料行 (的值為2。 如果 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC2，則函式會傳回 SQL_TIMESTAMP 欄位中 SQL_DATE、SQL_TIME 和 DATA_TYPE，COLUMN_SIZE 資料行包含近似數數值型別的十進位有效位數，而 NUM_PREC_RADIX 資料行包含值10。  
  
 當在呼叫 **SQLGetTypeInfo**時要求所有資料類型時，函數所傳回的結果集會包含 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP （如 odbc 3.x 中所 *定義），* 以及 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP （ *如 odbc 2.x*中所定義）。  
  
 由於 ODBC *3.X 驅動程式*管理員如何執行日期、時間和時間戳記資料類型（odbc 3）的對應 *。 x*驅動程式只需要在**SQLBindCol**和**SQLGetData**的*TargetType*引數中輸入的日期、時間和時間戳記 C 資料類型，以及**SQLBindParameter**的*ValueType*引數，即可辨識91、92和93的 **#defines** ，而且只需要辨識91、92和93的 **#defines** ，在**SQLBindParameter**的*ParameterType*引數或**SQLGetTypeInfo**的*DataType*引數中輸入的 SQL 資料類型。 如需詳細資訊，請參閱 [Datetime 資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
