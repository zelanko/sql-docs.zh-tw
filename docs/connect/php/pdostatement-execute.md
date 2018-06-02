---
title: 'Pdostatement:: Execute |Microsoft 文件'
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dabdabb4b3a4d20884004909dfaab0272f2e9c43
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34563866"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

執行陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>參數  
*$input*: （選擇性） 包含參數標記值的關聯陣列。  
  
## <a name="return-value"></a>傳回值  
成功時傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>備註  
以 PDOStatement::execute 執行的陳述式必須先使用 [PDO::prepare](../../connect/php/pdo-prepare.md)準備。 如需如何指定直接或已備妥陳述式執行的資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) 。  
  
輸入參數陣列的所有值都會被視為 PDO::PARAM_STR 值。  
  
如果已備妥的陳述式包含參數標記，您必須呼叫 PDOStatement::bindParam 以將 PHP 變數繫結至參數標記，或傳遞僅限輸入的參數值陣列。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
> [!NOTE]
> 建議使用字串做為輸入，當繫結至值[十進位或數值資料行](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)為確保如 PHP 有限的有效位數的有效位數和精確度[浮點數](http://php.net/manual/en/language.types.float.php)。 同樣適用於 bigint 資料行，尤其是有效值的範圍外[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
