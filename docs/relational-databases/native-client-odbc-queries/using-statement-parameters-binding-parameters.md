---
title: 系結參數 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 340a3a0f44201c81eafe8717962b2894709eb65d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73779530"
---
# <a name="using-statement-parameters---binding-parameters"></a>使用陳述式參數 - 繫結參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL 陳述式中的每一個參數標記都必須與應用程式的變數相關聯或繫結，才能執行該陳述式。 這是藉由呼叫[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)函數來完成。 **SQLBindParameter**描述驅動程式的程式變數（位址、C 資料類型等等）。 它也會藉由指定序數值以辨識參數標記，然後描述它所代表的 SQL 物件的特性 (SQL 資料類型、有效位數等)。  
  
 參數標記可以在執行陳述式之前的任何時候繫結或重新繫結。 在發生下列其中一個事件之前，參數繫結都會持續有效：  
  
-   呼叫[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md)並將*Option*參數設為 SQL_RESET_PARAMS 會釋出系結至語句控制碼的所有參數。  
  
-   呼叫**SQLBindParameter**並將*ParameterNumber*設定為系結參數標記的序數時，會自動釋放先前的系結。  
  
 應用程式也可以將參數繫結到程式變數的陣列，以批次的方式處理 SQL 陳述式。 陣列繫結有兩種類型：  
  
-   當每一個個別參數繫結到自己的變數陣列時，就會完成資料行取向繫結。  
  
     藉由呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)並將*屬性*設定為 SQL_ATTR_PARAM_BIND_TYPE，並將*valueptr 是*設定為 SQL_PARAM_BIND_BY_COLUMN 來指定資料行取向系結。  
  
-   當 SQL 陳述式的所有參數都是以單位的形式繫結到含有參數個別變數的結構陣列時，會形成資料列取向繫結。  
  
     藉由呼叫**SQLSetStmtAttr**並將*屬性*設定為 SQL_ATTR_PARAM_BIND_TYPE，並將*valueptr 是*設定為保留程式變數的結構大小，來指定資料列取向系結。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式將字元或二進位字串參數傳送至伺服器時，它會將值填補至**SQLBindParameter** *ColumnSize*參數中指定的長度。 如果 ODBC 2.x 應用程式為*ColumnSize*指定0，驅動程式會將參數值填補至資料類型的有效位數。 當連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器時，有效位數為 8000，連接至舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時則為 255。 Variant 資料行的*ColumnSize*是以位元組為單位。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援定義預存程序參數的名稱。 ODBC 3.5 也導入了對呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序時所使用之具名參數的支援。 這項支援可用來：  
  
-   呼叫預存程序，並提供為預存程序定義之參數子集的值。  
  
-   以不同的順序指定參數，也就是在應用程式中的順序，與在預存程序建立時所指定的順序不同。  
  
 只有在使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **execute**語句或 ODBC 呼叫 escape 序列來執行預存程式時，才支援具名引數。  
  
 如果為預存程式參數設定**SQL_DESC_NAME** ，則查詢中的所有預存程式參數也都應該設定**SQL_DESC_NAME**。  如果在預存程序呼叫中使用常值，其中參數已設定**SQL_DESC_NAME** ，則常值應使用格式 *' NAME*=*value*'，其中*name*是預存程式參數名稱（例如@p1）。 如需詳細資訊，請參閱[依名稱系結參數（具名引數）](https://go.microsoft.com/fwlink/?LinkId=167215)。  
  
## <a name="see-also"></a>另請參閱  
 [使用陳述式參數](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
  
