---
title: 'Pdostatement:: Bindparam |Microsoft Docs'
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65212058-2632-47a4-ba7d-2206883abf09
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9471c0c86edd9ff5a8357b797014036bd60fec83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647653"
---
# <a name="pdostatementbindparam"></a>PDOStatement::bindParam
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將參數繫結至 SQL 陳述式中的具名或問號預留位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::bindParam($parameter, &$variable[, $data_type[, $length[, $driver_options]]]);  
```  
  
#### <a name="parameters"></a>參數  
$*parameter*：(混合的) 參數識別碼。 若是使用具名預留位置的陳述式，使用參數名稱 (:name)。 如果是使用問號語法的已備妥陳述式，則會是以 1 起始的參數索引。  
  
&$*variable*：要繫結至 SQL 陳述式參數之 PHP 變數的 (混合) 名稱。  
  
$*data_type*：選擇性 (整數) PDO::PARAM_* 常數。 預設值是 PDO::PARAM_STR。  
  
$*length*：資料類型的選擇性 (整數) 長度。 您可以指定 PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE，以指出在 $*data_type* 中使用 PDO::PARAM_INT 或 PDO::PARAM_BOOL 時的預設大小。  
  
$*driver_options*： 選用 （混合） 驅動程式特有的選項。 例如，您可以指定 PDO::SQLSRV_ENCODING_UTF8，以 UTF-8 編碼的字串形式將資料行繫結至變數。  
  
## <a name="return-value"></a>傳回值  
如果成功，則為 TRUE，否則為 FALSE。  
  
## <a name="remarks"></a>Remarks  
將 Null 資料繫結至屬於 varbinary、binary 或 varbinary(max) 類型的伺服器資料行時，您應使用 $*driver_options* 指定二進位編碼 (PDO::SQLSRV_ENCODING_BINARY)。 如需編碼常數的詳細資訊，請參閱[常數](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  

## <a name="example"></a>範例  
此程式碼範例說明在 $contact 繫結至參數之後，變更值並將會使傳入查詢中的值隨之變更。  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindParam(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindParam(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```  
  
## <a name="example"></a>範例  
此程式碼範例說明如何存取輸出參數。  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$input1 = 'bb';  
  
$stmt = $conn->prepare("select ? = count(*) from Sys.tables");  
$stmt->bindParam(1, $input1, PDO::PARAM_STR, 10);  
$stmt->execute();  
echo $input1;  
?>  
```  
  
> [!NOTE]
> 時的輸出參數繫結至一個 bigint 型別，如果值可能超出範圍的最後[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)，pdo:: PARAM_INT 使用 pdo:: SQLSRV_PARAM_OUT_DEFAULT_SIZE 可能會導致 「 超出範圍的值 」 例外狀況。 因此，改為使用的預設值為 pdo:: PARAM_STR，並提供產生的字串，最多為 21 的大小。 它是數字，包括任何的 bigint 值的負號的最大數目。 

## <a name="example"></a>範例  
此程式碼範例說明如何使用輸入/輸出參數。  
  
```  
<?php  
   $database = "AdventureWorks";  
   $server = "(local)";  
   $dbh = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
   $dbh->query("IF OBJECT_ID('dbo.sp_ReverseString', 'P') IS NOT NULL DROP PROCEDURE dbo.sp_ReverseString");  
   $dbh->query("CREATE PROCEDURE dbo.sp_ReverseString @String as VARCHAR(2048) OUTPUT as SELECT @String = REVERSE(@String)");  
   $stmt = $dbh->prepare("EXEC dbo.sp_ReverseString ?");  
   $string = "123456789";  
   $stmt->bindParam(1, $string, PDO::PARAM_STR | PDO::PARAM_INPUT_OUTPUT, 2048);  
   $stmt->execute();  
   print $string;   // Expect 987654321  
?>  
```  

> [!NOTE]
> 建議使用字串做為輸入，繫結至的值時[十進位或數值資料行](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)若要確保精確性與正確性，如 PHP 有限精確度[浮點數](http://php.net/manual/en/language.types.float.php)。 這同樣適用於 bigint 資料行，尤其是值為範圍外[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。

## <a name="example"></a>範例  
此程式碼範例示範如何繫結十進位值做為輸入參數。  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```


## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
