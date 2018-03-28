---
title: PDOStatement::setFetchMode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f132b2af-0433-4fbe-b03f-69a7d631093a
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e63a4fe99dac224d858873660a6a493d498f9c88
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementsetfetchmode"></a>PDOStatement::setFetchMode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

指定 PDOStatement 控制代碼的擷取模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::setFetchMode( $mode );  
```  
  
#### <a name="parameters"></a>參數  
$*模式*： 任何能夠傳遞至參數[pdostatement:: Fetch](../../connect/php/pdostatement-fetch.md)。  
  
## <a name="return-value"></a>傳回值  
成功時傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt1 = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   while ( $row = $stmt1->fetch()) {   
      print($row['Name'] . "\n");   
   }  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_ASSOC);  
   $result = $stmt->fetch();  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_NUM);  
   $result = $stmt->fetch();  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_BOTH);  
   $result = $stmt->fetch();  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_LAZY);  
   $result = $stmt->fetch();  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->setFetchMode(PDO::FETCH_OBJ);  
   $result = $stmt->fetch();  
   print $result->Name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
