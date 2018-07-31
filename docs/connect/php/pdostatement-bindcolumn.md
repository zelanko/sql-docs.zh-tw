---
title: 'Pdostatement:: Bindcolumn |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b01f19dcb7b55da9c547d07d07784fe1730cdd66
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38006890"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將變數繫結至結果集內的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>參數  
$*column*：結果集內資料行的 (混合) 號碼 (以 1 起始的索引) 或資料行的名稱。  
  
&$*param*：資料行將繫結之 PHP 變數的 (混合) 名稱。  
  
$*type*：參數的選擇性資料類型 (以 PDO::PARAM_* 常數表示)。  
  
$*maxLen*：選擇性整數 (不是由 Microsoft Drivers for PHP for SQL Server 使用)。  
  
$*driverdata*：驅動程式的選擇性混合參數。 例如，您可以指定 PDO::SQLSRV_ENCODING_UTF8，以 UTF-8 編碼的字串形式將資料行繫結至變數。  
  
## <a name="return-value"></a>傳回值  
如果成功，傳回 TRUE，否則傳回 FALSE。  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例示範如何將變數繫結至結果集內的資料行。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
