---
title: sqlsrv_free_stmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_free_stmt
apitype: NA
helpviewer_keywords:
- sqlsrv_free_stmt
- API Reference, sqlsrv_free_stmt
ms.assetid: 3c71f432-36ad-41e1-8ac7-587c82539448
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fe1471d41bf7b510c52f584b538fde03d6c0c084
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802807"
---
# <a name="sqlsrvfreestmt"></a>sqlsrv_free_stmt
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

釋出所有與指定的陳述式相關聯的資源。 在呼叫此函數後，無法再次使用陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_free_stmt( resource $stmt)  
```  
  
#### <a name="parameters"></a>參數  
*$stmt*：要關閉的陳述式。  
  
## <a name="return-value"></a>傳回值  
除非使用無效的參數呼叫函數，否則為布林值 **true** 。 如果使用無效的參數呼叫函數，則傳回 **false** 。  
  
> [!NOTE]  
> **Null** 是此函數的有效參數。 這可讓函數在指令碼中多次呼叫。 例如，如果您在錯誤狀況下釋出陳述式，並且在指令碼結束時再次加以釋出，則在第二次呼叫 **sqlsrv_free_stmt** 時將會傳回 **true**，因為第一次呼叫 **sqlsrv_free_stmt** 時 (在錯誤狀況下) 已將陳述式資源設定為 **null**。  
  
## <a name="example"></a>範例  
下列範例會建立陳述式資源、執行簡單查詢，並呼叫 **sqlsrv_free_stmt** 以釋出所有與陳述式相關聯的資源。 此範例假設本機電腦上已安裝 SQL Server 和 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 資料庫。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM Person.Contact");  
if( $stmt )  
{  
     echo "Statement executed.\n";  
}  
else  
{  
     echo "Query could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*-------------------------------  
     Process query results here.  
-------------------------------*/  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  

[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)  
  
