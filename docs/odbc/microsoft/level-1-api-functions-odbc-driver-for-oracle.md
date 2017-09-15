---
title: "層級 1 API 函式 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3cd7f827ecfc367536654b9ad825302f4dba9fcf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>層級 1 API 函式 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 在此層級提供核心介面一致性函式加上其他功能，例如交易支援。  
  
|應用程式開發介面函式|注意|  
|------------------|-----------|  
|**SQLColumns**|建立結果集的資料表，這是指定之資料表的資料行清單或資料表。 當您要求的公用同義資料表資料行時，您必須設定 SYNONYMCOLUMNS 連接屬性，而且指定空字串做*szTableOwner*引數。 在傳回的公用同義字的資料行時，驅動程式會設定資料表名稱資料行設為空字串。 結果集包含的其他資料行序數位置，每個資料列的結尾。 這個值是資料行的資料表中的序數位置。|  
|**SQLDriverConnect**|連接到現有的資料來源。 如需詳細資訊，請參閱[連接字串格式和屬性](../../odbc/microsoft/connection-string-format-and-attributes.md)。|  
|**SQLGetConnectOption**|傳回連接選項的目前設定。 此函式僅部分支援。 此驅動程式支援的所有值*fOption*引數，但不支援某些*vParam*值*fOption*引數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). 如需詳細資訊，請參閱[連接選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLGetData**|擷取給定的結果集的目前記錄中的單一欄位的值。|  
|**SQLGetFunctions**|傳回所有支援的函式，則為 TRUE。 實作由驅動程式管理員。|  
|**SQLGetInfo**|傳回的資訊，包括 SQLHDBC、 SQLUSMALLINT、 SQLPOINTER、 SQLSMALLINT 和 SQLSMALLINT \*，ODBC Driver for Oracle 和資料來源連接控制代碼相關聯的相關*hdbc*。|  
|**SQLGetStmtOption**|傳回目前的陳述式選項的設定。 如需詳細資訊，請參閱[陳述式選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLGetTypeInfo**|傳回的資料來源所支援的資料類型的相關資訊。 驅動程式會傳回 SQL 結果集內的資訊。|  
|**SQLParamData**|搭配**SQLPutData**來指定參數資料在陳述式執行階段。|  
|**SQLPutData**|允許應用程式將參數或資料行的資料傳送到在陳述式執行階段的驅動程式。|  
|**SQLSetConnectOption**|提供存取管理方面的連線的選項。 此函式僅部分支援： 此驅動程式支援的所有值*fOption*引數，但不支援某些*vParam*值*fOption*引數[SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md)。 如需詳細資訊，請參閱[連接選項](../../odbc/microsoft/connect-options.md)。|  
|**SQLSetStmtOption**|設定選項相關的陳述式控制代碼， *hstmt*。 如需詳細資訊，請參閱[陳述式選項](../../odbc/microsoft/statement-options.md)。|  
|**SQLSpecialColumns**|擷取最佳的資料行集可唯一識別資料表中的資料列。|  
|**SQLStatistics**|擷取單一的資料表和索引或與資料表相關聯的標記名稱相關的統計資料的清單。 驅動程式會傳回結果集的資訊。|  
|**SQLTables**|傳回清單中的參數所指定的資料表名稱**SQLTables**陳述式。 如果未不指定任何參數，會傳回儲存在目前的資料來源中的資料表名稱。 驅動程式會傳回結果集的資訊。<br /><br /> 列舉型別呼叫不會接收結果集項目，檢視遠端或本機參數化的檢視。 不過，呼叫**SQLTables**與唯一資料表名稱規範會找到相符的這類檢視中，如果有的話，具有該名稱，這可讓 API 來檢查是否有之前建立新資料表的名稱衝突。<br /><br /> 公用的同義字會傳回 TABLE_OWNER 值是""。<br /><br /> SYS 或系統所擁有的檢視表會識別為系統檢視表。|
