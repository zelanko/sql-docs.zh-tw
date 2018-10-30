---
title: PDOStatement::fetchObject |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 71ad1932-cab3-4c29-8950-f5e82547d3b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3925dfab04904e347f5c8bc428c4de89b3c78e52
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655306"
---
# <a name="pdostatementfetchobject"></a>PDOStatement::fetchObject
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將下一個資料列擷取為物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
mixed PDOStatement::fetchObject([ $class_name[,$ctor_args ]] )  
```  
  
#### <a name="parameters"></a>參數  
$*class_name*：一個選擇性字串，指定要建立之類別的名稱。 預設值為 stdClass。  
  
$*ctor_args*：一個選擇性陣列，具有自訂類別建構函式的引數。  
  
## <a name="return-value"></a>傳回值  
如果成功，會傳回具有類別執行個體的物件。 屬性會對應至資料行。 如果失敗，會傳回 false。  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchObject();  
   print $result->Name;  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
