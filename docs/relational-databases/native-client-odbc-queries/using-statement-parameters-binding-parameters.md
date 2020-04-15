---
title: 繫結參數 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01e179d2abc6ef786f94b6d7938f0e21938c5a59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304621"
---
# <a name="using-statement-parameters---binding-parameters"></a>使用陳述式參數 - 繫結參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL 陳述式中的每一個參數標記都必須與應用程式的變數相關聯或繫結，才能執行該陳述式。 這是通過調用[SQLBind 參數](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)函數來完成的。 **SQLBind參數**向驅動程式描述程式變數(位址、C 資料類型等)。 它也會藉由指定序數值以辨識參數標記，然後描述它所代表的 SQL 物件的特性 (SQL 資料類型、有效位數等)。  
  
 參數標記可以在執行陳述式之前的任何時候繫結或重新繫結。 在發生下列其中一個事件之前，參數繫結都會持續有效：  
  
-   使用*選項*參數設置為SQL_RESET_PARAMS釋放綁定到語句句柄的所有參數的[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)的調用。  
  
-   對**SQLBind 參數**的呼叫,參數*編號*設置為綁定參數標記的定位,可自動釋放以前的綁定。  
  
 應用程式也可以將參數繫結到程式變數的陣列，以批次的方式處理 SQL 陳述式。 陣列繫結有兩種類型：  
  
-   當每一個個別參數繫結到自己的變數陣列時，就會完成資料行取向繫結。  
  
     按列方向綁定是透過調用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來指定的,*其屬性*設置為*SQL_ATTR_PARAM_BIND_TYPE,ValuePtr*設置為SQL_PARAM_BIND_BY_COLUMN。  
  
-   當 SQL 陳述式的所有參數都是以單位的形式繫結到含有參數個別變數的結構陣列時，會形成資料列取向繫結。  
  
     行綁定透過呼叫**SQLSetStmtAttr**來指定 *,其屬性*設定為SQL_ATTR_PARAM_BIND_TYPE,ValuePtr 設定為保存程式變數的結構*ValuePtr*的大小。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式向伺服器發送字元或二進位元字串參數時,它將值填充到**SQLBind 參數***列大小*參數中指定的長度。 如果 ODBC 2.x 應用程式為*ColumnSize*指定 0,則驅動程式將參數值填充到數據類型的精度。 當連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器時，有效位數為 8000，連接至舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時則為 255。 *列大小*是變體列的位元組。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援定義預存程序參數的名稱。 ODBC 3.5 也導入了對呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序時所使用之具名參數的支援。 這項支援可用來：  
  
-   呼叫預存程序，並提供為預存程序定義之參數子集的值。  
  
-   以不同的順序指定參數，也就是在應用程式中的順序，與在預存程序建立時所指定的順序不同。  
  
 僅當使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE**語句或 ODBC CALL 轉義序列執行儲存過程時,才支援命名參數。  
  
 如果為儲存過程參數設定了**SQL_DESC_NAME,** 則查詢中的所有儲存過程參數也應**SQL_DESC_NAME**設置。  如果在儲存過程呼叫中使用文字(其中參數已**SQL_DESC_NAME**設定),則文本應使用格式*為"name*=*值*",其中*名稱*是存儲過程參數名稱(例如@p1)。 有關詳細資訊,請參閱[按名稱(命名參數)綁定參數](https://go.microsoft.com/fwlink/?LinkId=167215)。  
  
## <a name="see-also"></a>另請參閱  
 [使用陳述式參數](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
