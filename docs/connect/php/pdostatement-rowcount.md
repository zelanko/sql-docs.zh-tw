---
title: "Pdostatement:: Rowcount |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0569f26a-2376-4c20-8813-bd3c87d0ae9f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e471f6f6ada3cd76bb3b0a3b373b13d7266eea37
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementrowcount"></a>PDOStatement::rowCount
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回最後一個陳述式所加入、刪除或變更的資料列數。  
  
## <a name="syntax"></a>語法  
  
```  
  
int PDOStatement::rowCount ();  
```  
  
## <a name="return-value"></a>傳回值  
加入、刪除或變更的資料列數。  
  
## <a name="remarks"></a>備註  
如果相關聯的 PDOStatement 所執行的最後一個 SQL 陳述式是 SELECT 陳述式，則 PDO::CURSOR_FWDONLY 資料指標會傳回 -1。 PDO::CURSOR_SCROLLABLE 資料指標會傳回結果集內的資料列數目。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例說明 rowCount 的兩種用法。 第一種用法會傳回已加入至資料表的資料列數目。 第二種用法說明 rowCount 可在您指定可捲動的資料指標時傳回結果集內的資料列數目。  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table2(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
  
echo "\n\n";  
  
$con = null;  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
print $stmt->rowCount();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

