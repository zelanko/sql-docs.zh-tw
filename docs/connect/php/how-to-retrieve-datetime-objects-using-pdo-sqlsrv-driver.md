---
title: 如何： 擷取為 PHP DateTime 物件，使用 PDO_SQLSRV 驅動程式的日期和時間類型 |Microsoft Docs
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
manager: mbarwin
ms.openlocfilehash: 54e5b5c9c1ba59ed64db740fbbb1a643e7cb1b2c
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676514"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdosqlsrv-driver"></a>如何： 擷取為 PHP DateTime 物件，使用 PDO_SQLSRV 驅動程式的日期和時間類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

使用 PDO_SQLSRV 驅動程式時，才有效這項功能，加入版本 5.6.0， [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>若要擷取做為 DateTime 物件的日期和時間類型

當使用 PDO_SQLSRV，日期和時間類型 (**smalldatetime**， **datetime**，**日期**，**時間**， **datetime2**，並**datetimeoffset**) 都預設以字串傳回。 PDO::ATTR_STRINGIFY_FETCHES 和 PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 屬性都不具有任何作用。 以日期和時間型別擷取為[PHP DateTime](http://php.net/manual/en/class.datetime.php)物件，設定的連接或陳述式屬性`PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE`來 **，則為 true** (它是**false**預設)。

> [!NOTE]
> 此連接或陳述式屬性僅適用於定期擷取的日期和時間型別因為 DateTime 物件不能指定為輸出參數。

## <a name="example---use-the-connection-attribute"></a>範例-使用連接屬性
下列範例會略過錯誤檢查為了清楚起見。 這個示範如何設定連接屬性：

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

## <a name="example---use-the-statement-attribute"></a>範例-使用陳述式屬性
此範例示範如何設定陳述式屬性：

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

## <a name="example---use-the-statement-option"></a>範例-使用陳述式選項
或者，陳述式屬性可以設定的選項：

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

## <a name="example---retrieve-datetime-types-as-strings"></a>範例-擷取日期時間型別為字串
下列範例示範如何達成相反 （這不是真的有必要因為它是預設為 false）：

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