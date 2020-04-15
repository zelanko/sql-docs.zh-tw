---
title: 日期時間資料類型 :微軟文件
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
ms.openlocfilehash: 10626c4f0bf2e33c70322a0eb49af6c3e01e4303
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307059"
---
# <a name="datetime-data-types"></a>日期時間資料類型
在 ODBC *3.x*中,日期、時間和時間戳 SQL 數據類型的標識符分別從 SQL_DATE、SQL_TIME和SQL_TIMESTAMP(標頭檔中的 **#define**實例為 9、10 和 11),更改為SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP(標頭檔中的 **#define**實例為 91、92 和 93)。 相應的 C 類型識別碼分別從SQL_C_DATE、SQL_C_TIME和SQL_C_TIMESTAMP更改為SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和**SQL_C_TYPE_TIMESTAMP,#define**實例也相應更改。  
  
 為 ODBC *3.x*中為 SQL 約會時間數據類型傳回的欄大小和十進位數字與在 ODBC *2.x*中為其傳回的精度和比例相同。 這些值與SQL_DESC_PRECISION和SQL_DESC_SCALE描述符欄位中的值不同。 (有關詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):資料類型。  
  
 這些更改會影響**SQL 描述科爾****、SQL 描述參數**和**SQLColattributes;****SQLBindCol、SQLBind****參數**和**SQLGetData;** 與**SQL 欄****、SQLGetTypeInfo、SQL****程式列****、SQL統計**與**SQL 特殊欄**。  
  
 ODBC *3.x*驅動程式根據SQL_ATTR_ODBC_VERSION環境屬性的設置處理上一段中列出的函數調用。 對於**SQLColumns、SQLGetTypeInfo、SQL****程式列****、SQL 特別列**和**SQLStatistics,** 如果SQL_ATTR_ODBC_VERSION設置為SQL_OV_ODBC3,則函數返回DATA_TYPE欄位**SQLColumns**中SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP。 COLUMN_SIZE列(在**SQLColumn、SQLGetTypeInfo、SQL****程式列**和**SQL 特別列**返回的結果集中)包含近似數值類型的二**SQLColumns**進位製精度。 NUM_PREC_RADIX列(在**SQLColumn、SQLGetTypeInfo**和**SQLColumns****SQL 過程列**返回的結果集中)包含值 2。 如果SQL_ATTR_ODBC_VERSION設置為SQL_OV_ODBC2,則函數返回DATA_TYPE欄位中的SQL_DATE、SQL_TIME和SQL_TIMESTAMP,則COLUMN_SIZE列包含近似數值類型的十進製精度,NUM_PREC_RADIX列包含值 10。  
  
 當在調用**SQLGetTypeInfo**時請求所有數據類型時,函數返回的結果集將包含 ODBC *3.x*中定義的SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP,以及 ODBC *2.x*中定義的SQL_DATE、SQL_TIME和SQL_TIMESTAMP。  
  
 由於 ODBC *3.x*驅動程式管理器如何對日期、時間和時間戳數據類型進行映射, ODBC *3.x*驅動程式只需要識別**SQLBindCol**和**SQLGetData***的 TargetType*參數或**SQLBind 參數***的值類型*參數中輸入的日期、時間和時間戳 C 數據類型 **#defines** 91、92 和 93,並且只需識別**在 SQLBind 參數***參數*或數據*類型*參數中輸入的日期、時間和時間戳**SQL**數據類型 **#defines** 91、92 和 93。 有關詳細資訊,請參閱[日期時間資料類型變更](../../../odbc/reference/develop-app/datetime-data-type-changes.md)。
