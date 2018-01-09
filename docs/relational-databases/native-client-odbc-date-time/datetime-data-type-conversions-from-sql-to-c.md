---
title: "從 SQL 轉換成 C |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36a60d790397b34ee66020fc3a174ba6df18ce63
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="datetime-data-type-conversions-from-sql-to-c"></a>從 SQL 到 C 的資料類型轉換的日期時間
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  下表將列出當您從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/時間類型轉換成 C 類型時應該考量的問題。  
  
## <a name="conversions"></a>轉換  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|@shouldalert|@shouldalert|@shouldalert|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|@shouldalert|@shouldalert|@shouldalert|  
|SQL_TYPE_DATE|[確定]|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|[確定]|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|[確定]|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|[確定]|21|16|16|  
  
## <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|[確定]|沒有轉換問題。|  
|@shouldalert|適用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的規則。|  
|2|忽略開頭和尾端空白。|  
|3|字串會剖析成日期、時間、時區或時區時差，而且小數秒數最多允許 9 位數。 如果剖析了時區時差，時間就會轉換成用戶端時區。 如果此轉換期間發生錯誤，將診斷記錄會產生含有 SQLSTATE 22018 和訊息 「 日期時間欄位溢位 」。|  
|4|如果此值不是有效的日期、時間戳記或時間戳記時差值，就會產生含有 SQLSTATE 22018 和訊息「轉換規格的字元值無效」的診斷記錄。|  
|5|如果時間不是零，就會產生含有 SQLSTATE 01S07 和訊息「小數位數截斷」的診斷記錄。|  
|6|如果此值不是有效的時間、時間戳記或時間戳記時差值，就會產生含有 SQLSTATE 22018 和訊息「轉換規格的字元值無效」的診斷記錄。|  
|7|忽略日期元件。|  
|8|如果小數秒數不是零，就會產生含有 SQLSTATE 01S07 和訊息「小數位數截斷」的診斷記錄。|  
|9|如果此值不是有效的日期、時間、時間戳記或時間戳記時差值，就會產生含有 SQLSTATE 22018 和訊息「轉換規格的字元值無效」的診斷記錄。|  
|10|如果此值是有效的時間，日期元件就會設定為目前的用戶端日期。|  
|11|如果此值是有效的日期，時間就會設定為零。|  
|12|產生含有 SQLSTATE 07006 和訊息「限制的資料類型屬性違規」的診斷記錄。|  
|13|時間會設定為零。|  
|14|如果緩衝區不夠大，無法容納 SQL_DATE_STRUCT，就會產生含有 SQLSTATE 22003 和訊息「數值超出範圍」的診斷記錄。|  
|15|日期會設定為目前的用戶端日期。|  
|16|如果緩衝區不夠大，無法容納轉換的字串，只能容納小數秒數，就會發生截斷，而且會產生含有 SQLSTATE 01004 和訊息「字串資料，右邊已截斷」的診斷記錄。 如果緩衝區不夠大，無法在不截斷日期、時間或時差元件的情況下容納字串值，就會產生含有 SQLSTATE 22003 和訊息「數值超出範圍」的診斷記錄。 請注意，若為日期和時間戳記時差，不可能會出現 SQLSTATE 01004，因為已轉換字串最右邊的部分不會包含小數秒數。 因此，任何截斷都會導致資料遺失。|  
|17|如果緩衝區不夠大，無法容納 SQL_SS_TIME2_STRUCT，就會產生含有 SQLSTATE 22003 和訊息「數值超出範圍」的診斷記錄。|  
|18|如果時間不是零，就會產生含有 SQLSTATE 01S07 和訊息「小數位數截斷」的診斷記錄。|  
|19|如果伺服器類型為 datetime 或 smalldatetime，則此值會對應至 TDS 電傳格式，而且將為 4 位元組值 (若為 smalldatetime) 和 8 位元組值 (若為 datetime)。<br /><br /> 如果伺服器類型是 datetime2，此值就會傳回成 SQL_TIMESTAMP_STRUCT。 如果緩衝區不夠大，無法容納傳回的值，就會產生含有 SQLSTATE 22003 和訊息「數值超出範圍」的診斷記錄。|  
|20|時間會轉換成用戶端時區。 如果進行這項轉換期間發生錯誤，就會產生含有 SQLSTATE 22008 和訊息「日期時間欄位溢位」的診斷記錄。|  
|21|如果緩衝區夠大，足以容納 SQL_SS_TIMESTAMPOFFSET_STRUCT，此值就會傳回成 SQL_SS_TIMESTAMPOFFSET_STRUCT。 否則，系統會產生含有 SQLSTATE 22003 和訊息「數值超出範圍」的診斷記錄。|  
|22|在擷取日期之前，此值會轉換成用戶端時區。 這樣做會在其他含有時間戳記時差類型的轉換中提供一致性。 如果進行這項轉換期間發生錯誤，就會產生含有 SQLSTATE 22008 和訊息「日期時間欄位溢位」的診斷記錄。 這可能會產生與簡單截斷所取得之值不同的日期。|  
  
 本主題中的表格描述傳回用戶端之類型與繫結中之類型之間的轉換。 輸出參數，如果在指定的伺服器類型 SQLBindParameter 不符合伺服器上的實際型別、 伺服器將會執行隱含的轉換和型別傳回至用戶端會比對透過 SQLBindParameter 中指定的型別。 當伺服器的轉換規則與上述表格中所列的規則不同時，這可能會導致非預期的轉換結果。 例如，必須提供預設日期時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 1900-1-1 而非目前的日期。  
  
## <a name="see-also"></a>請參閱  
 [日期和時間增強功能 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
