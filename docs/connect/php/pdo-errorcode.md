---
title: 'Pdo:: errorcode |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73bc57c0519c3371b77e38b00b7cc2a8a203b811
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37999188"
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode 會擷取資料庫控制代碼上最新作業的 SQLSTATE。  
  
## <a name="syntax"></a>語法  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>傳回值  
PDO::errorCode 會以字串形式傳回五字元的 SQLSTATE；如果沒有資料庫控制代碼的作業，則傳回 NULL。  
  
## <a name="remarks"></a>Remarks  
PDO_SQLSRV 驅動程式中的 PDO::errorCode 會針對某些成功的作業傳回警告。 例如，在成功連線之後，PDO::errorCode 會傳回 "01000"，指出 SQL_SUCCESS_WITH_INFO。  
  
PDO::errorCode 只會針對直接在資料庫連接上執行作業擷取錯誤碼。 如果您透過 PDO::prepare 或 PDO::query 建立 PDOStatement 執行個體，而陳述式物件產生錯誤，PDO::errorCode 不會擷取該錯誤。 您必須呼叫 PDOStatement::errorCode，才能傳回在特定陳述式物件上執行之作業的錯誤碼。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
在此範例中，資料行名稱的拼字錯誤 (`Cityx` 而不是 `City`)，因而導致錯誤並隨之進行報告。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
