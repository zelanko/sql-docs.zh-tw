---
description: 層級 1 API 函式 (ODBC Driver for Oracle)
title: 層級 1 API 函式 (ODBC Driver for Oracle) |Microsoft Docs
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
ms.openlocfilehash: 0c82ab0f481fbc60d0308895640371e84886e77e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483541"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>層級 1 API 函式 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 此層級的函式會提供核心介面一致性，外加額外的功能，例如交易支援。  
  
|API 函式|注意|  
|------------------|-----------|  
|**SQLColumns**|建立資料表的結果集，這是指定之資料表或資料表的資料行清單。 當您要求公用同義字的資料行時，您必須設定 SYNONYMCOLUMNS 連接屬性，並將空字串指定為 *szTableOwner* 引數。 傳回公用同義字的資料行時，驅動程式會將 [資料表名稱] 資料行設為空字串。 結果集會在每個資料列的結尾包含一個額外的資料行（序數位置）。 此值是資料表中資料行的序數位置。|  
|**SQLDriverConnect**|連接至現有的資料來源。 如需詳細資訊，請參閱 [連接字串格式和屬性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|傳回連接選項的目前設定。 部分支援此函式。 驅動程式支援*fOption*引數的所有值，但不支援*fOption*引數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 如需詳細資訊，請參閱 [連接選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|抓取給定結果集目前記錄中單一欄位的值。|  
|**SQLGetFunctions**|針對所有支援的函數傳回 TRUE。 由驅動程式管理員所執行。|  
|**SQLGetInfo**|傳回信息，包括 SQLHDBC、SQLUSMALLINT、SQLPOINTER、SQLSMALLINT 和 SQLSMALLINT \* ，關於 ODBC Driver For Oracle 和與連接控制碼 *hdbc*相關聯的資料來源。|  
|**SQLGetStmtOption**|傳回語句選項的目前設定。 如需詳細資訊，請參閱 [語句選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|傳回資料來源所支援資料類型的相關資訊。 驅動程式會傳回 SQL 結果集中的資訊。|  
|**SQLParamData**|與 **SQLPutData** 搭配使用，以在語句執行時間指定參數資料。|  
|**SQLPutData**|允許應用程式在語句執行時間，將參數或資料行的資料傳送至驅動程式。|  
|**SQLSetConnectOption**|提供管理連接層面之選項的存取權。 此函數為部分支援：驅動程式支援*fOption*引數的所有值，但不支援*fOption*引數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)的某些*vParam*值。 如需詳細資訊，請參閱 [連接選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|設定與語句控制碼 *hstmt*相關的選項。 如需詳細資訊，請參閱 [語句選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|抓取可在資料表中唯一識別資料列的最佳資料行集合。|  
|**SQLStatistics**|抓取與資料表相關聯的單一資料表和索引（或標記名稱）相關統計資料的清單。 驅動程式會以結果集的形式傳回信息。|  
|**SQLTables**|傳回 **SQLTables** 語句中參數所指定的資料表名稱清單。 如果未指定任何參數，則會傳回儲存在目前資料來源中的資料表名稱。 驅動程式會以結果集的形式傳回信息。<br /><br /> 列舉型別呼叫將不會收到遠端視圖或本機參數化視圖的結果集專案。 不過，使用唯一的資料表名稱規範來呼叫 **SQLTables** 時，會找到與該名稱相符的視圖（如果有的話）。這可讓 API 在建立新的資料表之前，檢查名稱是否衝突。<br /><br /> 公用同義字會以 "" TABLE_OWNER 值傳回。<br /><br /> SYS 或 SYSTEM 所擁有的視圖會識別為「系統檢視」。|
