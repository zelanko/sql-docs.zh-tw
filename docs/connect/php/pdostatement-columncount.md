---
title: PDOStatement::columnCount
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中的 PDOStatement::columnCount 函式適用的 API 參考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8d89a568-0c7c-40dd-9f54-db7313600df3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c1cfa12ea94a0ffd952473f13782e2bc49c4810
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645249"
---
# <a name="pdostatementcolumncount"></a>PDOStatement::columnCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回結果集內的資料行數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
int PDOStatement::columnCount ();  
```  
  
## <a name="return-value"></a>傳回值  
傳回結果集內的資料行數目。 如果結果集是空的，則傳回零。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
print $stmt->columnCount();   // 0  
  
echo "\n";  
$stmt->execute();  
print $stmt->columnCount();  
  
echo "\n";  
$stmt = $conn->query("select * from HumanResources.Department");  
print $stmt->columnCount();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
