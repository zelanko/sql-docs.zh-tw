---
title: 層級 1 API 函式（ODBC Driver for Oracle） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299948"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>層級 1 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 此層級的函式提供核心介面一致性，以及額外的功能，例如交易支援。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLColumns**|建立資料表的結果集，這是指定之資料表或資料表的資料行清單。 當您要求公用同義字的資料行時，您必須已設定 SYNONYMCOLUMNS 連接屬性，並指定空字串做為*szTableOwner*引數。 傳回公用同義字的資料行時，驅動程式會將 [資料表名稱] 資料行設定為空字串。 結果集會在每個資料列的結尾包含一個額外的資料行，也就是序數位置。 此值是資料表中資料行的序數位置。|  
|**SQLDriverConnect**|連接到現有的資料來源。 如需詳細資訊，請參閱[連接字串格式和屬性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|傳回連接選項的目前設定。 此函式是部分支援的功能。 此驅動程式支援*fOption*引數的所有值，但不支援*fOption*引數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 如需詳細資訊，請參閱[連接選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|在給定結果集的目前記錄中，抓取單一欄位的值。|  
|**SQLGetFunctions**|針對所有支援的函式傳回 TRUE。 由驅動程式管理員執行。|  
|**SQLGetInfo**|傳回信息，包括 SQLHDBC、SQLUSMALLINT、SQLPOINTER、SQLSMALLINT 和 SQLSMALLINT \*，關於 ODBC Driver for Oracle 和與連接控制碼（ *hdbc*）相關聯的資料來源。|  
|**SQLGetStmtOption**|傳回語句選項的目前設定。 如需詳細資訊，請參閱[語句選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|傳回資料來源所支援之資料類型的相關資訊。 驅動程式會傳回 SQL 結果集中的資訊。|  
|**SQLParamData**|與**SQLPutData**搭配使用，以在語句的執行時間指定參數資料。|  
|**SQLPutData**|允許應用程式在語句執行時間，將參數或資料行的資料傳送至驅動程式。|  
|**SQLSetConnectOption**|提供管理連接層面之選項的存取權。 此函式是部分支援的：此驅動程式支援*fOption*引數的所有值，但不支援*fOption*引數的某些*vParam*值[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)。 如需詳細資訊，請參閱[連接選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|設定與語句控制碼（ *hstmt*）相關的選項。 如需詳細資訊，請參閱[語句選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|抓取可唯一識別資料表中之資料列的最佳資料行集合。|  
|**SQLStatistics**|抓取關於單一資料表的統計資料清單，以及與資料表相關聯的索引或標記名稱。 驅動程式會以結果集的形式傳回信息。|  
|**SQLTables**|傳回**SQLTables**語句中的參數所指定的資料表名稱清單。 如果未指定任何參數，則會傳回儲存在目前資料來源中的資料表名稱。 驅動程式會以結果集的形式傳回信息。<br /><br /> 列舉類型呼叫將不會收到遠端查看或本機參數化視圖的結果集專案。 不過，以唯一資料表名稱規範呼叫**SQLTables**時，將會尋找具有該名稱之這類視圖的相符項（如果有的話）。這可讓 API 在建立新資料表之前，檢查名稱衝突。<br /><br /> 會傳回具有 TABLE_OWNER 值 "" 的公用同義字。<br /><br /> SYS 或 SYSTEM 所擁有的視圖會識別為系統檢視。|
