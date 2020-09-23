---
title: 如何：使用 PDO_SQLSRV 驅動程式以 PHP 日期時間物件形式擷取日期和時間類型
description: 本主題說明在使用 Microsoft PDO_SQLSRV Driver for PHP for SQL Server 時，如何以 PHP DateTime 物件的形式擷取日期和時間類型
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 507dc2a228419fb695d10a437681229ec6586f11
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680753"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdo_sqlsrv-driver"></a>如何：使用 PDO_SQLSRV 驅動程式以 PHP 日期時間物件形式擷取日期和時間類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此功能 (於 5.6.0 版中新增) 只有在使用適用於 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的 PDO_SQLSRV 驅動程式時才有效。

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>以 DateTime 物件形式擷取日期和時間類型

使用 PDO_SQLSRV 時，日期和時間類型 (**smalldatetime**、**datetime**、**date**、**time**、**datetime2** 及 **datetimeoffset**) 預設會以字串形式傳回。 PDO::ATTR_STRINGIFY_FETCHES 或 PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 屬性都不會有任何作用。 若要以 [PHP DateTime](http://php.net/manual/en/class.datetime.php) \(英文\) 物件的形式擷取日期和時間類型，請將連線或陳述式屬性 `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` 設定為 **true** (其預設為 **false**)。

> [!NOTE]
> 此連線或陳述式屬性僅適用於日期和時間類型的一般擷取，因為無法將 DateTime 物件指定為輸出參數。

## <a name="example---use-the-connection-attribute"></a>範例 - 使用連線屬性
為了清楚起見，下列範例會省略錯誤檢查。 此範例示範如何設定連線屬性：

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

## <a name="example---use-the-statement-attribute"></a>範例 - 使用陳述式屬性
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

## <a name="example---use-the-statement-option"></a>範例 - 使用陳述式選項
或者，也能以選項的形式設定陳述式屬性：

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

## <a name="example---retrieve-datetime-types-as-strings"></a>範例 - 以字串形式擷取日期時間類型
下列範例示範如何達成相反的情況 (這並非真的必要，因為其預設已為 false)：

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
