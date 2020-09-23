---
title: PDOStatement::closeCursor
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中的 PDOStatement::closeCursor 函式適用的 API 參考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61ced9d3c4dca42dfe71baaef1a3201fb4f2d260
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645329"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

關閉資料指標，使陳述式能夠再次執行。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>傳回值  
如果成功，則為 true，否則為 false。  
  
## <a name="remarks"></a>備註  
當 MultipleActiveResultSets 連接選項設為 false 時，closeCursor 會有效用。  如需 MultipleActiveResultSets 連線選項的詳細資訊，請參閱[如何：停用 Multiple Active Resultsets (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)。  
  
您也可以不要呼叫 closeCursor，而僅將陳述式控制代碼設為 Null。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
