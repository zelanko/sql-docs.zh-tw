---
title: sqlsrv_errors | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e097a5b89d708b3a91296c49c0c615f8955b96cb
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309047"
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回延伸錯誤及/或警告資訊有關上次**sqlsrv**執行作業。  
  
**Sqlsrv_errors**函式可以藉由呼叫與下方的 [參數] 區段中指定的參數值的其中一個傳回錯誤及/或警告資訊。  
  
根據預設，在呼叫任何 **sqlsrv** 函數時產生的警告會被視為錯誤；如果在呼叫 **sqlsrv** 函數時發生警告，此函數會傳回 false。 不過，對應至 SQLSTATE 值 01000、01001、01003 和 01S02 的警告絕不會被視為錯誤。  
  
以下這一行程式碼可關閉上述的行為；呼叫 **sqlsrv** 函數所產生的警告不會導致此函數傳回 false：  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
以下這一行程式碼可恢復預設行為；警告會被視為錯誤 (但有上述例外狀況)：  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
不論此設定，可以只擷取警告藉由呼叫**sqlsrv_errors**其中一種**SQLSRV_ERR_WARNINGS**或**SQLSRV_ERRORS**參數值 （請參閱參數面章節以取得詳細資料）。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>參數  
*$errorsAndOrWarnings*[選用]: 預先定義的常數。 此參數可以採用下表所列的其中一個值：  
  
|ReplTest1|描述|  
|---------|---------------|  
|SQLSRV_ERR_ALL|傳回上次呼叫 **sqlsrv** 函數時產生的錯誤和警告。|  
|SQLSRV_ERR_ERRORS|傳回上次呼叫 **sqlsrv** 函數時產生的錯誤。|  
|SQLSRV_ERR_WARNINGS|傳回上次呼叫 **sqlsrv** 函數時產生的警告。|  
  
如果未提供參數值，則會傳回上次呼叫 **sqlsrv** 函數時產生的錯誤和警告。  
  
## <a name="return-value"></a>傳回值  
陣列的 **array** ，或為 **null**。 每個**陣列**在傳回**陣列**包含三個索引鍵-值組。 下表列出每個索引鍵及其描述：  
  
|索引鍵|描述|  
|-------|---------------|  
|SQLSTATE|若為源自 ODBC 驅動程式的錯誤，則為 ODBC 所傳回的 SQLSTATE。 ODBC SQLSTATE 值的詳細資訊，請參閱[ODBC 錯誤碼](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。<br /><br />若為源自 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的錯誤，則為 IMSSP 的 SQLSTATE。<br /><br />若為源自 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的警告，則為 01SSP 的 SQLSTATE。|  
|代碼|若為源自 SQL Server 的錯誤，則為原生 SQL Server 錯誤碼。<br /><br />若為源自 ODBC 驅動程式的錯誤，則為 ODBC 所傳回的錯誤碼。<br /><br />對於源自 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的錯誤，則為 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 錯誤碼。 如需詳細資訊，請參閱 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)。|  
|message|錯誤的描述。|  
  
使用數值索引鍵 0、1 和 2 也可以存取陣列值。 如果未發生任何錯誤或警告，則會傳回 **null** 。  
  
## <a name="example"></a>範例  
下列範例顯示陳述式執行失敗時所發生的錯誤。 (陳述式會失敗，因為**InvalidColumName**不是有效的資料行名稱中指定的資料表。)此範例假設 SQL Server 和[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)資料庫安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
