---
title: 2 級 API 功能(Oracle 的 ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1e181c5863d6b906eaf9a3ba499728c595f0449
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284178"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>層級 2 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 此級別的函數提供 1 級介面一致性以及其他功能,如支援書籤、動態參數和非同步執行 ODBC 函數。  
  
|API 功能|注意|  
|------------------|-----------|  
|**SQLBindParameter**|將緩衝區與 SQL 語句中的參數標記關聯。|  
|**SQLBrowseConnect**|返回屬性和屬性值的連續級別。|  
|**SQLData來源**|列出數據源名稱。 由驅動程式管理員實施。|  
|**SQLDescribeParam**|返回與準備好的 SQL 語句關聯的參數標記的說明。<br /><br /> 返回基於分析語句的參數的最佳猜測。 如果無法確定參數類型,SQL_VARCHAR返回長度為 2000。|  
|**SQLDrivers**|由驅動程式管理員實施。|  
|**SQL 延伸**|與**SQLFetch**類似,但使用每個列的陣列返回多行。 結果集是可向前滾動的,如果游標定義為靜態的,而不是僅向前滾動,則可以向後滾動。 對於具有預設列綁定的僅轉發游標,大於 BUFFERSIZE 連接屬性的數據集的列數據將直接提取到數據緩衝區中。 不支援可變長度書籤,不支援從書籤的偏移量(0 以外的)提取行集。|  
|**SQLForeignKeys**|返回單個表中的外鍵清單,或引用單個表的其他表中的外鍵清單。|  
|**SQLMoreResults**|確定語句句柄(hstmt)上是否掛起更多結果,其中包含 SELECT、更新、插入或 DELETE 語句,如果是,則初始化這些結果的處理。<br /><br /> 使用 _結果集...|  
|**SQLNativeSql**|有關使用方式的資訊,請參閱[從儲存過程傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|傳回 SQL 語句中的參數數。 參數數應等於傳遞給**SQLPrepare**的 SQL 語句中的問號數。|  
|**SQLPrimaryKeys**|返回構成表主鍵的列名稱。|  
|**SQLProcedureColumns**|返回輸入和輸出參數的清單、返回值、單個過程的結果集中的列以及另外兩列「重載」和「ORDINAL_POSITION。 "重"是 Oracle 資料字典視圖ALL_ARGUMENTS表中的"重載"欄。 ORDINAL_POSITION是 Oracle 資料字典檢視ALL_ARGUMENTS表中的 SEQUENCE 列。 對於打包過程,程式名稱列採用*包名.程式名稱*格式。 不返回引用過程或函數的已創建同義詞的過程列。|  
|**SQLProcedures**|返回數據源中的過程清單。 對於打包過程,程式名稱列採用*包名.程式名稱*格式。<br /><br /> 由於 Oracle 不提供區分打包過程和打包函數的方法,因此驅動程式返回PROCEDURE_TYPE列SQL_PT_UNKNOWN。|  
|**SQLSetPos**|設置行集中的游標位置。 您可以將游標定位到行集中的特定行後,將**SQLSetPos**與**SQLGetData**一起從未綁定列中檢索列。 使用*fOption* SQL_ADD添加到結果集的行在結果集中的最後一行之後添加。|  
|**SQLSetScroll 選項**|設置控制與語句句柄 hstmt 關聯的游標行為的選項。 有關詳細資訊,請參閱[游標類型和併發組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
