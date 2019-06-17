---
title: 層級 2 API 函式 (ODBC Driver for Oracle) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be472a4a99324927128514fa9f8cbf19d44d49cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262252"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>層級 2 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 在此層級的函式提供層級 1 介面一致性加上額外的功能，例如支援書籤、 動態參數，以及非同步執行的 ODBC 函式。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLBindParameter**|關聯中的 SQL 陳述式的參數標記的緩衝區。|  
|**SQLBrowseConnect**|傳回屬性和屬性值的連續層的級。|  
|**SQLDataSources**|列出資料來源名稱。 實作由驅動程式管理員。|  
|**SQLDescribeParam**|傳回已備妥的 SQL 陳述式相關聯的參數標記的描述。<br /><br /> 傳回是哪些參數，以剖析陳述式的最佳的猜測。 如果無法判斷參數類型，長度 2000年傳回 SQL_VARCHAR。|  
|**SQLDrivers**|實作由驅動程式管理員。|  
|**SQLExtendedFetch**|類似於**SQLFetch**但會傳回每個資料行使用陣列的多個資料列。 結果集是順向可捲動，並可回溯可捲動資料指標會定義為靜態，不順如果。 預設資料行繫結使用順向資料指標，會直接將資料緩衝區擷取大於 BUFFERSIZE 連接屬性的資料集的資料行資料。 不支援可變長度的書籤，並不支援從書籤擷取資料列集 （不是 0) 的位移。|  
|**SQLForeignKeys**|傳回單一資料表或在單一資料表參考其他資料表中的外部索引鍵的清單中的外部索引鍵的清單。|  
|**SQLMoreResults**|判斷是否暫止更多的結果陳述式控制代碼，hstmt，其中包含 SELECT、 UPDATE、 INSERT 或 DELETE 陳述式，和如果是的話，會初始化這些結果的處理。<br /><br /> 使用 {resultset...} 逸出序列時，oracle 支援多個結果集只會從預存程序。|  
|**SQLNativeSql**|如需使用方式資訊，請參閱[從預存程序傳回陣列參數](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)。|  
|**SQLNumParams**|SQL 陳述式中傳回參數的數目。 參數的數目應該等於傳遞至 SQL 陳述式中的問號組成的數字**SQLPrepare**。|  
|**SQLPrimaryKeys**|傳回包含資料表的主索引鍵資料行名稱。|  
|**SQLProcedureColumns**|傳回輸入和輸出參數、 傳回值、 單一的程序中，結果集中的資料行和兩個額外的資料行，多載和 ORDINAL_POSITION 的清單。 多載是從 Oracle 資料字典檢視 ALL_ARGUMENTS 資料表的多載資料行。 ORDINAL_POSITION 是 SEQUENCE 資料行，從 Oracle 資料字典檢視 ALL_ARGUMENTS 資料表。 封裝的程序，程序名稱資料行所在*packagename.procedurename*格式。 不會傳回參考程序或函式建立同義字的程序資料行。|  
|**SQLProcedures**|傳回資料來源中的程序的清單。 封裝的程序，程序名稱資料行所在*packagename.procedurename*格式。<br /><br /> 因為 Oracle 不提供用來在封裝的程序區別封裝函式，則驅動程式會傳回 SQL_PT_UNKNOWN PROCEDURE_TYPE 資料行。|  
|**SQLSetPos**|設定資料列集中的資料指標位置。 您可以使用**SQLSetPos**具有**SQLGetData**未繫結的資料行中擷取資料列之後的特定資料列遊標定位在資料列集中。 加入到結果集使用的資料列*fOption* SQL_ADD 加入結果集內的最後一個資料列之後。|  
|**SQLSetScrollOptions**|設定控制陳述式控制代碼，hstmt 相關聯的資料指標行為的選項。 如需詳細資訊，請參閱 <<c0> [ 資料指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|
