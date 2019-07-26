---
title: '如何: 使用 Windows 驗證進行連接 |Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84707c67491d4f02be41e6506fb233ee7afef9fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936500"
---
# <a name="how-to-connect-using-windows-authentication"></a>如何：使用 Windows 驗證進行連接
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

根據預設， [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 使用 Windows 驗證來連接 SQL Server。 請務必注意，在大部分情況下，這表示網頁伺服器的處理序身分識別或執行緒身分識別 (如果網頁伺服器使用模擬) 用來連接伺服器，而非使用者的身分識別。  
  
當您使用 Windows 驗證來連接 SQL Server 時，必須考量下列幾點：  
  
-   用以執行 Web 伺服器的處理序 (或執行緒) 的認證必須對應到有效的 SQL Server 登入，才能建立連接。  
  
-   如果 SQL Server 和 Web 伺服器位於不同的電腦，必須設定 SQL Server 以啟用遠端連接。  
  
> [!NOTE]  
> 當您建立連接時，可以設定 *Database* 和 *ConnectionPooling* 等連接屬性。 如需支援之連接屬性的完整清單，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
  
可能的話，Windows 驗證應該用來連接 SQL Server，原因如下：  
  
-   在驗證期間不會透過網路傳遞任何認證；使用者名稱和密碼不會內嵌在資料庫連接字串中。 這表示惡意使用者或攻擊者無法藉由監視網路或檢視組態檔內的連接字串來取得認證。  
  
-   使用者受制於集中式帳戶管理；會強制執行安全性原則，例如；密碼到期日、最小密碼長度，以及帳戶在多次無效登入要求後鎖定。  
  
如果 Windows 驗證不是實際的選項，請參閱 [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md)。  
  
## <a name="example"></a>範例  
使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的 SQLSRV 驅動程式，下列範例會使用 Windows 驗證來連接 SQL Server 的本機執行個體。 建立連接之後，會向伺服器查詢正在存取資料庫之使用者的登入。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從瀏覽器執行範例時，所有輸出都會寫入至瀏覽器。  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>範例  
下列範例使用 PDO_SQLSRV 驅動程式來完成與前一個範例相同的工作。  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[如何：使用 SQL Server 驗證進行連線](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[如何：建立 SQL Server 登入](../../relational-databases/security/authentication-access/create-a-login.md)

[如何：建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)

[管理使用者、角色和登入](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[使用者結構描述分隔](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[授與物件權限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
