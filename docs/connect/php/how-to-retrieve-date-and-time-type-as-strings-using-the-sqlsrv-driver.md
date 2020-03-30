---
title: 使用 SQLSRV 驅動程式以字串形式擷取日期和時間類型 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as strings
ms.assetid: 58a974ea-4daf-4e3b-98ed-9731b9c9250f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8c3fbd475d5f7038d36ba17a9578713c3ed1b53
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993526"
---
# <a name="how-to-retrieve-date-and-time-types-as-strings-using-the-sqlsrv-driver"></a>如何：使用 SQLSRV 驅動程式以字串形式擷取日期和時間類型
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

針對 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 使用 SQLSRV 驅動程式時，您可以在連接字串中或於陳述式層級指定下列選項，來以字串形式擷取日期和時間類型 (**smalldatetime**、**datetime**、**date**、**time**、**datetime2** 及 **datetimeoffset**)：

```
'ReturnDatesAsStrings'=>true
```

預設值是 **false**，表示 **smalldatetime**、**datetime**、**date**、**time**、**datetime2** 與 **datetimeoffset** 等類型將會以 [PHP DateTime](http://php.net/manual/en/class.datetime.php) 物件的形式傳回。 如果此選項是於陳述式層級設定，其會覆寫連線層級設定。

PDO_SQLSRV 驅動程式預設會以字串形式傳回日期和時間類型。 若要以 PHP DateTime 物件的形式加以擷取，請參閱[如何：使用 PDO_SQLSRV 以 PHP DateTime 物件形式擷取日期和時間類型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)

## <a name="example"></a>範例
下列範例說明指定要以字串的形式擷取日期和時間類型的語法。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings '=> true);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_close($conn);
?>
```

## <a name="example"></a>範例
下列範例說明您可以在擷取字串時指定 UTF-8，以字串的形式擷取日期，即使在透過 `"ReturnDatesAsStrings" => false` 建立連接時亦然。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", "ReturnDatesAsStrings" => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING("UTF-8"));

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;

sqlsrv_close($conn);
?>
```

## <a name="example"></a>範例
下列範例說明如何藉由在連接字串中指定 UTF-8 和 `"ReturnDatesAsStrings" => true`，以字串的形式擷取日期。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks", 'ReturnDatesAsStrings'=> true, "CharacterSet" => 'utf-8');
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as string
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

echo $date;
sqlsrv_close($conn);
?>
```

## <a name="example"></a>範例
下列範例說明如何以 PHP 類型的形式擷取日期。 `'ReturnDatesAsStrings'=> false` 。

```php
<?php
$serverName = "MyServer";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tsql = "SELECT VersionDate FROM AWBuildVersion";

$stmt = sqlsrv_query($conn, $tsql);

if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}

sqlsrv_fetch($stmt);

// retrieve date as a DateTime object, then convert to string using PHP's date_format function
$date = sqlsrv_get_field($stmt, 0);

if ($date === false) {
   die(print_r(sqlsrv_errors(), true));
}

$date_string = date_format($date, 'jS, F Y');
echo "Date = $date_string\n";

sqlsrv_close($conn);
?>
```

## <a name="example"></a>範例
陳述式層級的 ReturnDatesAsStrings 選項會覆寫相對應的連線選項。

```php
<?php
$serverName = 'MyServer';
$connectionInfo = array('Database' => 'MyDatabase', 'ReturnDatesAsStrings' => false);
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
   echo "Could not connect.\n";
   die(print_r(sqlsrv_errors(), true));
}

$tableName = 'MyTable';
$options = array('ReturnDatesAsStrings' => true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
if ($stmt === false) {
   echo "Error in statement preparation/execution.\n";
   die(print_r(sqlsrv_errors(), true));
}
sqlsrv_execute($stmt);

// Expect the fetched value to be a string
$field = sqlsrv_get_field($stmt, 0);
echo $field . PHP_EOL;

sqlsrv_close($conn);
?>
```

## <a name="see-also"></a>另請參閱
[擷取資料](../../connect/php/retrieving-data.md)

[操作說明：使用 PDO_SQLSRV 以 PHP DateTime 物件形式擷取日期和時間類型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)
