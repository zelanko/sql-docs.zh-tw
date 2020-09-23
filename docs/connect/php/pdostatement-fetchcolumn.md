---
title: PDOStatement::fetchColumn
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中的 PDOStatement::fetchColumn 函式適用的 API 參考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6ebf385c-ddb0-4c53-9dc6-7df0d3740b04
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cbfc332339e3cd5e17890ef3a7ef9341474a8189
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645081"
---
# <a name="pdostatementfetchcolumn"></a>PDOStatement::fetchColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回資料列中的一個資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
string PDOStatement::fetchColumn ([ $column_number ] );  
```  
  
#### <a name="parameters"></a>參數  
$*column_number*：一個選擇性整數，表示以零起始的資料行編號。 預設值為 0 (資料列中的第一個資料行)。  
  
## <a name="return-value"></a>傳回值  
一個資料行，如果沒有更多資料列則為 false。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   while ( $result = $stmt->fetchColumn(1)) {   
      print($result . "\n");   
   }  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
