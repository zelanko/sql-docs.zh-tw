---
title: 從 C 轉換成 SQL |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4f9fe3c7f5753788df339484bbf29e2d6e953dba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030436"
---
# <a name="datetime-data-type-conversions-from-c-to-sql"></a>datetime 資料類型從 C 轉換成 SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主題列出問題需要考量當您從 C 類型轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期/時間類型。  
  
 下表描述的轉換會套用到用戶端上進行的轉換。 在其中用戶端指定的參數不同於伺服器上定義的小數秒有效位數的情況下，用戶端轉換可能會成功，但是伺服器會傳回錯誤時**SQLExecute**或**SQLExecuteDirect**呼叫。 特別是，ODBC 會將任何截斷的小數秒視為錯誤，而[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]行為是要捨入，例如四捨五入時，就會從**datetime2(6)** 到**datetime2(2)** . Datetime 資料行值會捨去為一秒的 1/300，而 smalldatetime 資料行的秒數會由伺服器設定為零。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|N/A|N/A|1,10,11|N/A|N/A|N/A|N/A|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|N/A|N/A|N/A|N/A|1,10,11|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|N/A|N/A|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|N/A|N/A|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|N/A|N/A|N/A|N/A|N/A|N/A|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|  
  
## <a name="key-to-symbols"></a>符號的索引鍵  
  
-   **-** ：不支援轉換。 產生含有 SQLSTATE 07006 和訊息「限制的資料類型屬性違規」的診斷記錄。  
  
-   **1**:如果提供的資料無效，就會產生含有 SQLSTATE 22007 和訊息「無效的 datetime 格式」的診斷記錄。  
  
-   **2**:時間欄位必須為零，否則會產生含有 SQLSTATE 22008 和訊息「小數截略」的診斷記錄。  
  
-   **3**:小數秒數必須為零，否則會產生含有 SQLSTATE 22008 和訊息「小數截略」的診斷記錄。  
  
-   **4**：忽略日期元件。  
  
-   **5**：時區會設定為用戶端的時區設定。  
  
-   **6**：時間會設定為零。  
  
-   **7**:日期會設定為目前的日期。  
  
-   **8**:時間是從用戶端的時區轉換為 UTC。 如果進行這項轉換期間發生錯誤，就會產生含有 SQLSTATE 22008 和訊息「日期時間欄位溢位」的診斷記錄。  
  
-   **9**:根據出現的第一個標點符號字元以及剩餘的元件是否存在，字串會經過剖析，並轉換為 date、datetime、datetimeoffset 或 time 值。 接著，在此程序探索來源類型之先前資料表中的規則之後，此字串會轉換為目標類型。 如果在剖析資料時偵測到錯誤，就會產生含有 SQLSTATE 22018 和訊息「轉換規格的字元值無效」的診斷記錄。 對於 datetime 和 smalldatetime 參數，如果年份超出這些類型支援的範圍，就會產生含有 SQLSTATE 22007 和訊息「無效的 datetime 格式」的診斷記錄。  
  
     對於 datetimeoffset，即使沒有要求轉換為 UTC，此值在轉換到 UTC 之後仍然必須在範圍內。 這是因為 TDS 和伺服器永遠會以 UTC 的 datetimeoffset 值，將時間正規化，因此用戶端必須在轉換成 UTC 之後，確認時間元件位於支援的範圍內。 如果此值不在支援的 UTC 範圍內，就會產生含有 SQLSTATE 22007 和訊息「無效的 datetime 格式」的診斷記錄。  
  
-   **10**:如果截斷時發生資料遺失，就會產生含有 SQLSTATE 22008 和訊息「無效的時間格式」的診斷記錄。 如果此值落在伺服器使用之 UTC 範圍所代表的範圍外，也可能發生這個錯誤。  
  
-   **11**:如果資料的位元組長度不等於 SQL 類型所要求的結構大小，就會產生含有 SQLSTATE 22003 和訊息「數值超出範圍」的診斷記錄。  
  
-   **12**:如果資料的位元組長度為 4 或 8，資料會以原始的 TDS smalldatetime 或 datetime 格式，傳送到伺服器。 如果資料的位元組長度完全符合 SQL_TIMESTAMP_STRUCT 的大小，資料就會轉換成適用於 datetime2 的 TDS 格式。  
  
-   **13**:如果截斷時發生資料遺失，就會產生含有 SQLSTATE 22001 和訊息「字串資料，右邊已截斷」的診斷記錄。  
  
     從根據下表的目的地資料行的大小決定小數秒位數 （小數位數） 的數目：  
  
    ||||  
    |-|-|-|  
    |type|隱含的小數位數<br /><br /> 0|隱含的小數位數<br /><br /> 1..9|  
    |SQL_C_TYPE_TIMESTAMP|19|21..29|  
  
     不過對於 SQL_C_TYPE_TIMESTAMP，如果可以用三位數代表小數秒而不會造成資料遺失，而且資料行大小為 23 以上，則會產生完整的三位數小數秒。 此行為可確保使用舊版 ODBC 驅動程式所開發之應用程式的回溯相容性。  
  
     對於大於資料表中範圍的資料行大小，會隱含小數位數 9。 此轉換應該最多允許九個小數秒位數，也就是 ODBC 所允許的最大值。  
  
     資料行大小為零暗示 ODBC 中變數長度字元類型的大小無限制 (除非 SQL_C_TYPE_TIMESTAMP 套用 3 位數規則，否則為 9 位數)。 利用固定的長度字元類型將資料行大小指定為零是錯誤。  
  
-   **N/A**:系統會維持現有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和舊有的行為。  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
