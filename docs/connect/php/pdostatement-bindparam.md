---
title: PDOStatement::bindParam | Microsoft Docs
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
ms.openlocfilehash: cd3332f9dc12d1cf7df22c097ab9370606985a68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936159"
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
  
$*driver_options*: 選擇性 (混合) 驅動程式特有的選項。 例如，您可以指定 PDO::SQLSRV_ENCODING_UTF8，以 UTF-8 編碼的字串形式將資料行繫結至變數。  
  
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
> 將輸出參數系結至 Bigint 型別時, 如果值的結尾可能超出[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)的範圍, 使用 pdo::P ARAM_INT 搭配 pdo:: SQLSRV_PARAM_OUT_DEFAULT_SIZE 可能會產生「值超出範圍」例外狀況。 因此, 請改為使用預設的 PDO::P ARAM_STR, 並提供所產生字串的大小, 最多為21。 這是任何 Bigint 值的最大數位數目, 包括負號。 

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
> 建議在將值繫結至 [decimal 或 numeric 資料行](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)時使用字串作為輸入，以確保精確度與正確性，因為 PHP 所具備的[浮點數](https://php.net/manual/en/language.types.float.php) \(英文\) 精確度有限。 這同樣適用於 bigint 資料行，尤其當值不在某個[整數](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)的範圍內時。

## <a name="example"></a>範例  
此程式碼範例示範如何繫結十進位值作為輸入參數。  

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

[PDO](https://php.net/manual/book.pdo.php)  
  
