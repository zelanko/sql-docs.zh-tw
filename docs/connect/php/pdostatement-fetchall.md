---
title: PDOStatement::fetchAll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: be74188a-77cd-4d19-b16e-77278373c979
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7126c36e098b724b3c0920e384c95e75a2181e37
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799167"
---
# <a name="pdostatementfetchall"></a>PDOStatement::fetchAll
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

以陣列方式傳回結果集內的資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
array PDOStatement::fetchAll([ $fetch_style[, $column_index ][, ctor_args]] );  
```  
  
#### <a name="parameters"></a>參數  
$*fetch_style*：(整數) 符號，用於指定資料列資料的格式。 如需值清單，請參閱 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) 。 也允許 PDO::FETCH_COLUMN。 PDO::FETCH_BOTH 是預設值。  
  
$*column_index*：整數值，代表 $*fetch_style* 為 PDO::FETCH_COLUMN 時所要傳回的資料行。 0 是預設值。  
  
$*ctor_args*：當 $*fetch_style* 為 PDO::FETCH_CLASS 或 PDO::FETCH_OBJ 時，類別建構函式的參數陣列。  
  
## <a name="return-value"></a>傳回值  
結果集內剩餘的資料列陣列，如果方法呼叫失敗，則傳回 false。  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_BOTH);  
   print_r( $result );  
   print "\n-----------\n";  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_NUM);  
   print_r( $result );  
   print "\n-----------\n";  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_COLUMN, 1);  
   print_r( $result );  
   print "\n-----------\n";  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg\n";  
      }  
  
      function __toString() {  
         echo "To string\n";  
      }  
   };  
  
   $stmt = $conn->query( 'SELECT TOP(2) * FROM Person.ContactType' );  
   $all = $stmt->fetchAll( PDO::FETCH_CLASS, 'cc', array( 'Hi!' ));  
   var_dump( $all );  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
