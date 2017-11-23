---
title: "層級 2 應用程式開發介面函式 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6232a890c5898bcf543df9e47c97f363e2bfca12
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>層級 2 應用程式開發介面函式 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 在此層級的函式提供層級 1 介面一致性加上額外的功能，例如支援書籤、 動態參數，以及 ODBC 函數的非同步執行。  
  
|應用程式開發介面函式|注意|  
|------------------|-----------|  
|**SQLBindParameter**|緩衝區關聯的 SQL 陳述式中的參數標記。|  
|**SQLBrowseConnect**|傳回後續的層級的屬性和屬性值。|  
|**SQLDataSources**|列出資料來源名稱。 實作由驅動程式管理員。|  
|**SQLDescribeParam**|傳回已備妥的 SQL 陳述式相關聯的參數標記的描述。<br /><br /> 傳回是何種參數，根據剖析陳述式的最佳的猜測。 如果無法判別參數類型，長度 2000年傳回 SQL_VARCHAR。|  
|**SQLDrivers**|實作由驅動程式管理員。|  
|**SQLExtendedFetch**|類似於**SQLFetch**但傳回每個資料行使用陣列的多個資料列。 結果集是順向可捲動且可進行回溯可捲動資料指標定義為靜態，不是順如果。 以預設資料行繫結順向資料指標，直接將資料緩衝區會不提取大於 BUFFERSIZE 連接屬性的資料集的資料行資料。 不支援可變長度的書籤，並不支援從書籤擷取資料列集 （不是 0) 的位移。|  
|**SQLForeignKeys**|傳回單一資料表或在單一資料表參考其他資料表中的外部索引鍵的清單中的外部索引鍵的清單。|  
|**SQLMoreResults**|判斷是否暫止多個結果的陳述式控制代碼，hstmt，其中包含 SELECT、 UPDATE、 INSERT 或 DELETE 陳述式並若是如此，初始化這些結果的處理。<br /><br /> Oracle 支援多個結果集只會從預存程序，使用 {resultset...} 逸出序列時。|  
|**SQLNativeSql**|如需使用方式資訊，請參閱[從預存程序傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|SQL 陳述式中傳回參數的數目。 參數的數目應該等於傳遞至 SQL 陳述式中的問號數目**SQLPrepare**。|  
|**SQLPrimaryKeys**|傳回組成資料表主索引鍵資料行名稱。|  
|**SQLProcedureColumns**|傳回輸入和輸出參數、 傳回值，單一的程序中，結果集中的資料行和兩個額外的資料行，多載和 ORDINAL_POSITION 的清單。 多載會從 Oracle 資料字典檢視 ALL_ARGUMENTS 資料表的多載資料行。 ORDINAL_POSITION 是時序資料行，從 Oracle 資料字典檢視 ALL_ARGUMENTS 資料表。 封裝的程序，該程序名稱資料行是*packagename.procedurename*格式。 不會傳回建立的同義字參考的程序或函式的程序資料行。|  
|**SQLProcedures**|傳回資料來源中的程序的清單。 封裝的程序，該程序名稱資料行是*packagename.procedurename*格式。<br /><br /> 因為 Oracle 不提供封裝函式從區別封裝的程序的方法，驅動程式會傳回 SQL_PT_UNKNOWN PROCEDURE_TYPE 資料行。|  
|**SQLSetPos**|設定資料列集中的資料指標位置。 您可以使用**SQLSetPos**與**SQLGetData**後資料列集定位資料指標到特定的資料列，從解除繫結的資料行中擷取資料列。 資料列加入到結果集使用*fOption* SQL_ADD 會在結果集中的最後一個資料列之後加入。|  
|**SQLSetScrollOptions**|設定控制陳述式控制代碼，hstmt 相關聯的資料指標行為的選項。 如需詳細資訊，請參閱[資料指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
