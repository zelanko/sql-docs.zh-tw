---
title: 如何：使用 SQL Server 驗證進行連接 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, SQL Server Authentication
ms.assetid: 8d298830-3186-47e7-aef6-586b457901c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10028beb86526f553a959376804d855513f0336c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916444"
---
# <a name="how-to-connect-using-sql-server-authentication"></a>How to: Connect Using SQL Server Authentication
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支援在您連接到 SQL Server 時使用 SQL Server 驗證。  
  
在無法使用 Windows 驗證時，才應該使用 SQL Server 驗證。 如需使用 Windows 驗證進行連接的相關資訊，請參閱 [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md)。  
  
當您使用 SQL Server 驗證連接到 SQL Server 時，必須考量以下幾點：  
  
-   必須在伺服器上啟用 SQL Server 混合模式驗證。  
  
-   當您嘗試建立連接時，必須設定使用者識別碼和密碼 (SQLSRV 驅動程式中的 *UID* 和 *PWD* 連接屬性)。 使用者識別碼和密碼必須對應至有效的 SQL Server 使用者和密碼。  
  
> [!NOTE]  
> 包含右大括號 (}) 的密碼必須以第二個右大括號逸出。 例如，如果 SQL Server 密碼為 "pass}word"，則 *PWD* 連接屬性的值必須設為 "pass}}word"。  
  
當您使用 SQL Server 驗證連接到 SQL Server 時，應採取下列預防措施：  
  
-   保護 (加密) 透過網路從 Web 伺服器傳遞至資料庫的認證。 從 SQL Server 2005 開始，認證依預設會加密。 為提高安全性，可將「加密連接」屬性設為「開啟」，以對所有傳送至伺服器的資料進行加密。  
  
> [!NOTE]  
> 將「加密連接」屬性設為「開啟」可能會降低效能，因為資料加密可能會耗用大量運算資源。  
  
-   請不要在 PHP 指令碼中以純文字的形式加入連接屬性 *UID* 和 *PWD* 的值。 這些值應以受到限制的適當權限儲存在應用程式特定目錄中。  
  
-   請避免使用 *sa* 帳戶。 請將應用程式對應至具有所需權限、並使用強式密碼的資料庫使用者。  
  
> [!NOTE]  
> 當您建立連接時，可以設定使用者識別碼和密碼以外的連接屬性。 如需支援之連接屬性的完整清單，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
  
## <a name="example"></a>範例  
下列範例會 SQLSRV 驅動程式，透過 Windows 驗證連接到 SQL Server 的本機執行個體。 必要的 *UID* 和 *PWD* 連接屬性值，會從位於 *C:\AppData* 目錄中的應用程式特定文字檔 *uid.txt* 和 *pwd.txt* 中取用。 在建立連接之後，將會查詢伺服器以確認使用者登入。  
  
此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從瀏覽器執行範例時，所有輸出都會寫入至瀏覽器。  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
  
/* Get UID and PWD from application-specific files.  */  
$uid = file_get_contents("C:\AppData\uid.txt");  
$pwd = file_get_contents("C:\AppData\pwd.txt");  
$connectionInfo = array( "UID"=>$uid,  
                         "PWD"=>$pwd,  
                         "Database"=>"AdventureWorks");  
  
/* Connect using SQL Server Authentication. */  
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
此範例會使用 PDO_SQLSRV 驅動程式示範如何透過 SQL Server 驗證進行連接。  
  
```  
<?php  
   $serverName = "(local)";   
   $database = "AdventureWorks";  
  
   // Get UID and PWD from application-specific files.   
   $uid = file_get_contents("C:\AppData\uid.txt");  
   $pwd = file_get_contents("C:\AppData\pwd.txt");  
  
   try {  
      $conn = new PDO( "sqlsrv:server=$serverName;Database = $database", $uid, $pwd);   
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
  
   // Free statement and connection resources.   
   $stmt = null;   
   $conn = null;   
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[如何：使用 SQL Server 驗證進行連線](../../connect/php/how-to-connect-using-sql-server-authentication.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)

[SUSER_SNAME (Transact-SQL)](../../t-sql/functions/suser-sname-transact-sql.md)

[如何：建立 SQL Server 登入](../../relational-databases/security/authentication-access/create-a-login.md)

[如何：建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)

[管理使用者、角色和登入](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[使用者結構描述分隔](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[授與物件權限 (Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
