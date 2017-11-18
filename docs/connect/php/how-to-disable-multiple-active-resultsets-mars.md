---
title: "如何： 停用 Multiple Active Resultsets (MARS) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 641b6ed54cf668aee1218b05fda1a5c3c792d409
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>如何：停用 Multiple Active Resultsets (MARS)。
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

如果您需要連接到未啟用 Multiple Active Result Sets (MARS) 的 SQL Server 資料來源，您可以使用 MultipleActiveResultSets 連接選項來停用或啟用 MARS。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-disable-mars-support"></a>停用 MARS 支援  
  
-   使用下列連接選項：  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    如果您的應用程式嘗試在連接上執行具有開啟的作用中結果集的查詢，第二個查詢嘗試將會傳回下列錯誤資訊：  
  
    連接無法處理這項作業，因為有某個陳述式具有擱置的結果。  若要讓連接可供其他查詢使用，請擷取所有結果，並取消或釋放陳述式。 如需 MultipleActiveResultSets 連接的詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
  
## <a name="example"></a>範例  
下列範例說明如何使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的 SQLSRV 驅動程式停用 MARS 支援。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>範例  
下列範例示範如何停用 MARS 支援使用 PDO_SQLSRV 驅動程式的[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[連接到伺服器](../../connect/php/connecting-to-the-server.md)  
  

