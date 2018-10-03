---
title: sqlsrv_server_info |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_server_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_server_info
- sqlsrv_server_info
ms.assetid: ef6fe2b7-d267-4379-b948-5626c4684367
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca2dd9e131a2c8b07945fdd4bf3d5afd2c5ebc4f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596967"
---
# <a name="sqlsrvserverinfo"></a>sqlsrv_server_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回伺服器的相關資訊。 呼叫此函數之前，必須先建立連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_server_info( resource $conn)  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：用以連接用戶端與伺服器的連接資源。  
  
## <a name="return-value"></a>傳回值  
具有下列索引鍵的關聯陣列：  
  
|索引鍵|Description|  
|-------|---------------|  
|CurrentDatabase|目前做為目標的資料庫。|  
|SQLServerVersion|SQL Server 的版本。|  
|SQLServerName|伺服器的名稱。|  
  
## <a name="example"></a>範例  
從命令列執行下列範例時，該範例會將伺服器資訊寫入主控台。  
  
```  
<?php  
/* Connect to the local server using Windows Authentication. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$server_info = sqlsrv_server_info( $conn);  
if( $server_info )  
{  
      foreach( $server_info as $key => $value)  
      {  
             echo $key.": ".$value."\n";  
      }  
}  
else  
{  
      echo "Error in retrieving server info.\n";  
      die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
