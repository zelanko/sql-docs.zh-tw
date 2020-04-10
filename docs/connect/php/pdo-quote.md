---
title: PDO::quote | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db661eea0ea4b3b46e3a73f7e1f4609267bbae41
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919064"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將引號放在基礎 SQL Server 資料庫所需的輸入字串前後，以處理查詢中使用的字串。 PDO::quote 將使用適合 SQL Server 的引號樣式，逸出輸入字串中的特殊字元。  
  
## <a name="syntax"></a>語法  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>參數  
$*string*：要加上引號的字串。  
  
$*parameter_type*：指出資料類型的選擇性 (整數) 符號。  預設值是 PDO::PARAM_STR。  

PHP 7.2 引進了新的 PDO 常數，以新增[繫結 Unicode 和非 Unicode 字串](https://wiki.php.net/rfc/extended-string-types-for-pdo) \(英文\) 的支援。 Unicode 字串可以用引號括住，並以 N 作為前置詞 (例如 N'string'，而不是 'string')。

1. PDO::PARAM_STR_NATL - 適用於 Unicode 字串的新類型，以位元 OR 的形式套用至 PDO::PARAM_STR
1. PDO::PARAM_STR_CHAR - 適用於非 Unicode 字串的新類型，以位元 OR 的形式套用至 PDO::PARAM_STR
1. PDO::ATTR_DEFAULT_STR_PARAM - 設定為 PDO::PARAM_STR_NATL 或 PDO::PARAM_STR_CHAR 以表示以位元 OR 的形式套用至 PDO::PARAM_STR 的預設值

從版本 5.8.0 開始，可以搭配 PDO::quote 使用這些常數。
  
## <a name="return-value"></a>傳回值  
可以傳遞至 SQL 陳述式的加上引號的字串，如果失敗則傳回 false。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="example"></a>範例  

下列指令碼顯示了一些範例，這些範例說明擴充字串類型如何影響 PHP 7.2+ 的 PDO::quote()。

```
<?php
$database = "test";
$server = "(local)";
$db = new PDO("sqlsrv:server=$server; Database=$database", "", "");

$db->quote('über', PDO::PARAM_STR | PDO::PARAM_STR_NATL); // N'über'
$db->quote('foo'); // 'foo'

$db->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$db->quote('über'); // N'über'
$db->quote('foo', PDO::PARAM_STR | PDO::PARAM_STR_CHAR); // 'foo'
?>
```
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
