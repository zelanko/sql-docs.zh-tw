---
title: 如何：使用 PDO_SQLSRV 驅動程式以 PHP 日期時間物件形式擷取日期和時間類型 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 165e91cee3b0b4592f9b746f8b35b46bc73bce50
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264572"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>如何：使用 PDO_SQLSRV 驅動程式以 PHP 日期時間物件形式擷取日期和時間類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

這項功能在版本5.6.0 版中新增, 只有在使用的 PDO_SQLSRV 驅動程式[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]時才有效。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>將日期和時間類型取出為 DateTime 物件

使用 PDO_SQLSRV 時, 日期和時間類型 (**Smalldatetime**、 **datetime**、 **date**、 **time**、 **datetime2**和**datetimeoffset**) 預設會以字串傳回。 PDO:: ATTR_STRINGIFY_FETCHES 或 PDO:: SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 屬性都不會有任何作用。 若要將日期和時間類型取出為[PHP DateTime](http://php.net/manual/en/class.datetime.php)物件, 請將 connection 或語句屬性`PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE`設定為**true** (預設為**false** )。

> [!NOTE]
> 此連接或語句屬性僅適用于日期和時間類型的一般提取, 因為 DateTime 物件不能指定為 output 參數。

## <a name="example---use-the-connection-attribute"></a>範例-使用連接屬性
下列範例會省略錯誤檢查以清楚瞭解。 這個範例顯示如何設定連接屬性:

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>範例-使用語句屬性
這個範例顯示如何設定語句屬性:

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>範例-使用語句選項
或者, 您也可以將語句屬性設定為選項:

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>範例-將日期時間類型取出為字串
下列範例示範如何達到相反的情況 (這不是真正必要的, 因為它預設為 false):

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>另請參閱
[擷取資料](../../connect/php/retrieving-data.md)

[使用 SQLSRV 驅動程式以字串形式擷取日期和時間類型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)