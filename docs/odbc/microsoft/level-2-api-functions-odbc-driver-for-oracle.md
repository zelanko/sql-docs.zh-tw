---
title: 層級 2 API 函式（ODBC Driver for Oracle） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284178"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>層級 2 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 此層級的函式提供層級1介面一致性，以及額外的功能，例如支援書簽、動態參數和 ODBC 函數的非同步執行。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLBindParameter**|將緩衝區與 SQL 語句中的參數標記產生關聯。|  
|**SQLBrowseConnect**|傳回連續的屬性和屬性值層級。|  
|**SQLDataSources**|列出資料來源名稱。 由驅動程式管理員執行。|  
|**SQLDescribeParam**|傳回與備妥的 SQL 語句相關聯之參數標記的描述。<br /><br /> 根據剖析語句，傳回參數的最佳猜測。 如果無法判斷參數類型，SQL_VARCHAR 會傳回，其長度為2000。|  
|**SQLDrivers**|由驅動程式管理員執行。|  
|**SQLExtendedFetch**|類似于**SQLFetch** ，但會針對每個資料行使用陣列來傳回多個資料列。 如果將資料指標定義為靜態，而不是順向，則結果集會向前復原，而且可以回溯滾動。 針對具有預設資料行系結的順向資料指標，大於 BUFFERSIZE 連接屬性之資料集的資料行資料會直接提取到資料緩衝區中。 不支援可變長度的書簽，也不支援從書簽提取位移（不是0）的資料列集。|  
|**SQLForeignKeys**|傳回單一資料表中的外鍵清單，或參考單一資料表之其他資料表中的外鍵清單。|  
|**SQLMoreResults**|判斷語句控制碼（hstmt）上是否有更多的結果暫止，包含 SELECT、UPDATE、INSERT 或 DELETE 子句，如果是，則會初始化這些結果的處理。<br /><br /> 使用 {resultset ...} escape 序列時，Oracle 只支援預存程式的多個結果集。|  
|**SQLNativeSql**|如需使用方式的詳細資訊，請參閱[從預存程式傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|傳回 SQL 語句中的參數數目。 參數的數目應該等於傳遞給**SQLPrepare**的 SQL 語句中的問號數目。|  
|**SQLPrimaryKeys**|傳回組成資料表主鍵的資料行名稱。|  
|**SQLProcedureColumns**|傳回輸入和輸出參數的清單、傳回值、單一程式結果集中的資料行，以及兩個額外的資料行，多載和 ORDINAL_POSITION。 多載是 Oracle 資料字典視圖的 ALL_ARGUMENTS 資料表中的多載資料行。 ORDINAL_POSITION 是來自 Oracle 資料字典視圖之 ALL_ARGUMENTS 資料表的 SEQUENCE 資料行。 針對封裝的程式，程式名稱資料行是*packagename. 程式名稱*格式。 不會傳回參考程式或函數之已建立同義字的程式資料行。|  
|**SQLProcedures**|傳回資料來源中的程式清單。 針對封裝的程式，程式名稱資料行是*packagename. 程式名稱*格式。<br /><br /> 因為 Oracle 並未提供方式來區別封裝函式的封裝程式，所以驅動程式會針對 PROCEDURE_TYPE 資料行傳回 SQL_PT_UNKNOWN。|  
|**SQLSetPos**|設定資料列集中的資料指標位置。 將資料指標定位至資料列集中的特定資料列之後，您可以使用**SQLSetPos**搭配**SQLGetData** ，從未系結的資料行中取出資料列。 使用*fOption* SQL_ADD 加入至結果集的資料列會加入結果集的最後一個資料列之後。|  
|**SQLSetScrollOptions**|設定選項來控制與語句控制碼（hstmt）相關聯之資料指標的行為。 如需詳細資訊，請參閱資料[指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
