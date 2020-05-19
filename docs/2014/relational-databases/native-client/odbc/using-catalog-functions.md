---
title: 使用目錄函數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9308f9208d75287f3c93112f7f810c8ece3bc18b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704270"
---
# <a name="using-catalog-functions"></a>使用目錄函數
  所有資料庫都有包含儲存在資料庫之資料的結構。 此結構的定義以及權限之類的其他資訊會儲存在目錄 (當做一組系統資料表實作) 中，也就是所謂的資料字典。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式可讓應用程式透過呼叫 ODBC 目錄函數來判斷資料庫結構。 目錄函數會在結果集中傳回資訊，而且會使用目錄預存程序進行實作以便查詢目錄中的系統資料表。 例如，應用程式可能要求的結果集包含系統上所有資料表，或是特定資料表中所有資料行的相關資訊。 標準 ODBC 目錄函數用於取得應用程式所連接之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的目錄資訊。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援分散式查詢，其中來自多個異質 OLE DB 資料來源的資料會以單一查詢進行存取。 存取遠端 OLE DB 資料來源的其中一個方法是將資料來源定義為連結伺服器。 您可以使用[sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)來完成這項作業。 在定義連結伺服器之後，您可以在 Transact-SQL 陳述式中使用四部份名稱來參考該伺服器中的物件：  
  
 *linked_server_name. catalog. schema. object_name*。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援兩種驅動程式專用的函數，可協助取得連結伺服器的目錄資訊：  
  
-   **SQLLinkedServers**  
  
     傳回在本機伺服器上定義的連結伺服器清單。  
  
-   **SQLLinkedCatalogs**  
  
     傳回連結伺服器中所包含的目錄清單。  
  
 當您擁有連結的伺服器名稱和目錄名稱之後， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式支援使用兩部分名稱的_linked_server_name_從目錄中取得資訊 **。** 下列 ODBC 目錄函數的*CatalogName* _目錄_：  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 兩部分_linked_server_name_**。**[SQLForeignKeys](../../native-client-odbc-api/sqlforeignkeys.md)上的*FKCatalogName*和*sqlforeignkeys*也支援_目錄_。  
  
 使用 SQLLinkedServers 和 SQLLinkedCatalogs 需要下列檔案：  
  
-   sqlncli.h  
  
     包括適用於連結伺服器目錄函數的函數原型與常數定義。 sqlncli.h 必須包含在 ODBC 應用程式中，而且必須在應用程式編譯時的 Include 路徑中。  
  
-   sqlncli11.lib  
  
     必須位於連結器 (Linker) 的程式庫路徑中，並指定為要連結的檔案。 sqlncli11.lib 是透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式散發。  
  
-   sqlncli11.dll  
  
     在執行時間必須存在。 sqlncli11.dll 是透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式散發。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../statistics/statistics.md)  
  
  
