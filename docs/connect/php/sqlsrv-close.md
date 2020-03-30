---
title: sqlsrv_close | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_close
apitype: NA
helpviewer_keywords:
- sqlsrv_close
- API Reference, sqlsrv_close
ms.assetid: 6ac6209c-a134-4f8f-b88b-8eefaa1cbc7f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b4610cfd971c7de8f729902bc09237b47e19dad
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67935819"
---
# <a name="sqlsrv_close"></a>sqlsrv_close
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

關閉指定的連接，並釋放相關聯的資源。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_close( resource $conn )  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：要關閉的連接。  
  
## <a name="return-value"></a>傳回值  
除非使用無效的參數呼叫函數，否則為布林值 **true** 。 如果使用無效的參數呼叫函數，則傳回 **false** 。  
  
> [!NOTE]  
> **Null** 是此函數的有效參數。 這可讓函數在指令碼中多次呼叫。 例如，如果您在錯誤狀況下關閉連線，並且在指令碼結束時再次加以關閉，則在第二次呼叫 **sqlsrv_close** 時將會傳回 **true**，因為第一次呼叫 **sqlsrv_close** 時 (在錯誤狀況下) 會將連線資源設定為 **null**。  
  
## <a name="example"></a>範例  
下列範例會關閉連接。 此範例假設 SQL Server 安裝在本機電腦上。 從命令列執行範例時，所有輸出都會寫入至主控台。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection here.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
echo "Connection closed.\n";  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[關於文件中的程式碼範例](../../connect/php/about-code-examples-in-the-documentation.md)  
  
