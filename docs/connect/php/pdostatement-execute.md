---
title: PDOStatement::execute | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d6918a70217e7b98100bdc514edf65622e30b1a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909054"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

執行陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>參數  
*$input*：(選擇性) 包含參數標記值的關聯陣列。  
  
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
> 建議在將值繫結至 [decimal 或 numeric 資料行](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)時使用字串作為輸入，以確保精確度與正確性，因為 PHP 所具備的[浮點數](https://php.net/manual/en/language.types.float.php) \(英文\) 精確度有限。 這同樣適用於 bigint 資料行，尤其當值不在某個[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)的範圍內時。

## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
