---
title: 日期時間資料類型變更 :微軟文件
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
ms.openlocfilehash: 4f186047dd31aa2c4b66ec1ce73c8cb9fae31c04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304641"
---
# <a name="datetime-data-type-changes"></a>Datetime 資料類型變更
在 ODBC *3.x*中,日期、時間和時間戳 SQL 數據類型的標識符分別從 SQL_DATE、SQL_TIME和SQL_TIMESTAMP(標頭檔中的 **#define**實例為 9、10 和 11),更改為SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP(標頭檔中的 **#define**實例為 91、92 和 93)。 相應的 C 類型識別碼分別從SQL_C_DATE、SQL_C_TIME和SQL_C_TIMESTAMP更改為SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 和SQL_C_TYPE_TIMESTAMP。  
  
 為 ODBC *3.x*中為 SQL 約會時間數據類型傳回的欄大小和十進位數字與在 ODBC *2.x*中為其傳回的精度和比例相同。 這些值與SQL_DESC_PRECISION和SQL_DESC_SCALE描述符欄位中的值不同。 (關於詳細資訊,請參閱[欄大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 這些更改會影響**SQL 描述科爾****、SQL 描述Param**和**SQLColattribute;****SQLBindCol、SQLBind****參數**和**SQLGetData;** 與**SQL 欄****、SQLGetTypeInfo、SQL****程式列****、SQL統計**與**SQL 特殊欄**。  
  
 下表顯示了 ODBC *3.x*驅動程式管理器如何對**SQLBindCol**和**SQLGetData** *的 TargetType*參數或**SQLBind 參數***的值類型*參數中輸入的日期、時間和時間戳 C 數據類型進行映射。  
  
|資料類型<br /><br /> 輸入的代碼|*2.x*應用程式到<br /><br /> *2.x*驅動程式|*2.x*應用程式到<br /><br /> *3.x*驅動程式|*3.x*應用程式到<br /><br /> *2.x*驅動程式|*3.x*應用程式到<br /><br /> *3.x*驅動程式|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|無對應|SQL_C_TYPE_DATE (91)|無映射[1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|錯誤(來自 DM)|錯誤(來自 DM)|SQL_C_DATE (9)|無映射[2]|  
|SQL_C_TIME (10)|無對應|SQL_C_TYPE_TIME (92)|無映射[1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|錯誤(來自 DM)|錯誤(來自 DM)|SQL_C_TIME (10)|無映射[2]|  
|SQL_C_TIMESTAMP (11)|無對應|SQL_C_TYPE_TIMESTAMP (93)|無映射[1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|錯誤(來自 DM)|錯誤(來自 DM)|SQL_C_TIMESTAMP (11)|無映射[2]|  
  
 [1] 因此,使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式可以使用目錄函數傳回的結果集中返回的日期、時間或時間戳碼。  
  
 [2] 因此,使用 ODBC *3.x*驅動程式的 ODBC *3.x*應用程式可以使用目錄函數傳回的結果集中返回的日期、時間或時間戳碼。  
  
 下表顯示了 ODBC *3.x*驅動程式管理員如何對**SQLBind 參數**的*參數類型*參數或**SQLGetTypeInfo**的*資料類型*參數中輸入的日期、時間和時間戳 SQL 資料類型進行映射。  
  
|資料類型<br /><br /> 輸入的代碼|*2.x*應用程式到<br /><br /> *2.x*驅動程式|*2.x*應用程式到<br /><br /> *3.x*驅動程式|*3.x*應用程式到<br /><br /> *2.x*驅動程式|*3.x*應用程式到<br /><br /> *3.x*驅動程式|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|無對應|SQL_TYPE_DATE (91)|無映射[1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|錯誤(來自 DM)|錯誤(來自 DM)|SQL_DATE (9)|無映射[2]|  
|SQL_TIME (10)|無對應|SQL_TYPE_TIME (92)|無映射[1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|錯誤(來自 DM)|錯誤(來自 DM)|SQL_TIME (10)|無映射[2]|  
|SQL_TIMESTAMP (11)|無對應|SQL_TYPE_TIMESTAMP (93)|無映射[1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|錯誤(來自 DM)|錯誤(來自 DM)|SQL_TIMESTAMP (11)|無映射[2]|  
  
 [1] 因此,使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式可以使用目錄函數傳回的結果集中返回的日期、時間或時間戳碼。  
  
 [2] 因此,使用 ODBC *3.x*驅動程式的 ODBC *3.x*應用程式可以使用目錄函數傳回的結果集中返回的日期、時間或時間戳碼。
