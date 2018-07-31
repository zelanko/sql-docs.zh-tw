---
title: PDOStatement::debugDumpParams |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf156d65-d933-4235-b89a-18e172d61c15
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f26207c153581999904b7b1dd574c17b4f2eb66
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992800"
---
# <a name="pdostatementdebugdumpparams"></a>PDOStatement::debugDumpParams
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

顯示已備妥的陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::debugDumpParams();  
```  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = "Owner";  
  
$stmt = $conn->prepare("select * from Person.ContactType where name = :param");  
$stmt->execute(array($param));  
$stmt->debugDumpParams();  
  
echo "\n\n";  
  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->execute(array($param));  
$stmt->debugDumpParams();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
