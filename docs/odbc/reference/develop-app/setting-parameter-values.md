---
title: 設定參數值 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 923fd57f4308fb72aca2f829ccb9d7b884c12546
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299828"
---
# <a name="setting-parameter-values"></a>設定參數值
要設置參數的值,應用程式只需設置綁定到參數的變數的值。 設置此值時並不重要,只要在執行語句之前設置此值。 應用程式可以在綁定變數之前或之後設置該值,並且它可以根據需要多次更改該值。 執行語句時,驅動程式只需檢索變數的當前值。 當已準備好的語句執行多次時,這特別有用;應用程式在每次執行語句時為部分或全部變數設置新值。 有關此示例,請參閱本節前面[部的"準備執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)"。  
  
 如果在呼叫**SQLBind 參數**時綁定了長度/指示器緩衝區,則必須在執行語句之前將其設置為以下值之一:  
  
-   綁定變數中數據的位元組長度。 僅當變數為字元或二進位變數 *(ValueType*為SQL_C_CHAR或SQL_C_BINARY)時,驅動程式才會檢查此長度。  
  
-   SQL_NTS 資料是一個 null 端接的字串。  
  
-   SQL_NULL_DATA 資料值為 NULL,驅動程式忽略綁定變數的值。  
  
-   SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的結果。 參數的值將與**SQLPutData**一起發送。 有關詳細資訊,請參閱在本部份的後面部份[送出長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 下表顯示了綁定變數的值以及應用程式為各種參數值設置的長度/指示器緩衝區。  
  
|參數<br /><br /> value|參數<br /><br /> (SQL)<br /><br /> 資料類型|變數 (C)<br /><br /> 資料類型| 中的值<br /><br /> 繫結<br /><br /> 變動| 中的值<br /><br /> 長度/指示器<br /><br /> 緩衝區[d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC[0[a]|SQL_NTS或 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10[0]a]|SQL_NTS或 2|  
|下午1時|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0[b]|--|  
|下午1時|SQL_TYPE_TIME|SQL_C_CHAR|{t '13:00:00'{0}a},{c}|SQL_NTS或 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0"表示空終止字元。 僅當長度/指示器緩衝區中的值SQL_NTS時,才需要空終止字元。  
  
 [b] 此清單中的數位是存儲在TIME_STRUCT結構欄位中的數位。  
  
 [c] 字串使用 ODBC 日期轉義子句。 關於詳細資訊,請參閱[日期、時間與時間戳文字](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 驅動程式必須始終檢查此值以查看它是否是特殊值,如SQL_NULL_DATA。  
  
 驅動程式在執行時使用參數值時所做的與驅動程序無關。 如有必要,驅動程式將值從綁定變數的 C 資料類型和位元組長度轉換為參數的 SQL 資料類型、精度和比例。 在大多數情況下,驅動程式然後將值發送到數據源。 在某些情況下,它將該值格式化為文本,並將其插入到 SQL 語句中,然後再將該語句發送到數據源。
