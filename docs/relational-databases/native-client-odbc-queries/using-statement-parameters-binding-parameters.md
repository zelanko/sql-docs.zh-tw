---
title: 繫結參數 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6d51c8cb13a4a8bd2e9cc14e8208c6d9e0e0084f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-statement-parameters---binding-parameters"></a>使用陳述式參數的繫結參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQL 陳述式中的每一個參數標記都必須與應用程式的變數相關聯或繫結，才能執行該陳述式。 這是藉由呼叫[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)函式。 **SQLBindParameter**描述驅動程式之程式變數 （位址、 C 資料類型，等等）。 它也會藉由指定序數值以辨識參數標記，然後描述它所代表的 SQL 物件的特性 (SQL 資料類型、有效位數等)。  
  
 參數標記可以在執行陳述式之前的任何時候繫結或重新繫結。 在發生下列其中一個事件之前，參數繫結都會持續有效：  
  
-   呼叫[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)與*選項*參數設定為 SQL_RESET_PARAMS，釋出所有的參數繫結至陳述式控制代碼。  
  
-   呼叫**SQLBindParameter**與*Sqlbindparameter*設定為繫結的參數標記的序數會自動釋放之前的繫結。  
  
 應用程式也可以將參數繫結到程式變數的陣列，以批次的方式處理 SQL 陳述式。 陣列繫結有兩種類型：  
  
-   當每一個個別參數繫結到自己的變數陣列時，就會完成資料行取向繫結。  
  
     資料行取向繫結會指定藉由呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)與*屬性*設為 SQL_ATTR_PARAM_BIND_TYPE 和*ValuePtr*設為 SQL_PARAM_BIND_BY_COLUMN。  
  
-   當 SQL 陳述式的所有參數都是以單位的形式繫結到含有參數個別變數的結構陣列時，會形成資料列取向繫結。  
  
     資料列取向繫結會指定藉由呼叫**SQLSetStmtAttr**與*屬性*設為 SQL_ATTR_PARAM_BIND_TYPE 和*ValuePtr*設結構保留大小程式變數。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會將字元或二進位字串參數傳送到伺服器，它將值填補至指定的長度**SQLBindParameter** *ColumnSize*參數。 如果 ODBC 2.x 應用程式指定 0 代表*ColumnSize*，驅動程式會填補到資料類型的精確度的參數值。 當連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器時，有效位數為 8000，連接至舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時則為 255。 *ColumnSize*變數資料行的位元組。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援定義預存程序參數的名稱。 ODBC 3.5 也導入了對呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序時所使用之具名參數的支援。 這項支援可用來：  
  
-   呼叫預存程序，並提供為預存程序定義之參數子集的值。  
  
-   以不同的順序指定參數，也就是在應用程式中的順序，與在預存程序建立時所指定的順序不同。  
  
 使用時，才會支援具名的參數[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE**陳述式或 ODBC CALL 逸出序列執行預存程序。  
  
 如果**SQL_DESC_NAME**設定預存程序參數，在查詢中的所有預存程序參數也應該設定**SQL_DESC_NAME**。  如果常值會使用在預存程序呼叫中，其中參數已**SQL_DESC_NAME**設定，則常值應該使用格式 *' 名稱*=*值*'，其中*名稱*是預存程序的參數名稱 (例如， @p1)。 如需詳細資訊，請參閱[依名稱 （具名參數） 的繫結參數](http://go.microsoft.com/fwlink/?LinkId=167215)。  
  
## <a name="see-also"></a>另請參閱  
 [使用陳述式參數](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
