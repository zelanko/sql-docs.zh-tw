---
title: 將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)
description: 了解在使用 PDO_SQLSRV 驅動程式時，如何使用 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 和 SQLSRV_ATTR_DECIMAL_PLACES 屬性將十進位值或貨幣值格式化
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae61b239fca2a923645b9de963309c62a3919b3d
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680653"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

為了維持正確性，[decimal 或 numeric 類型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)一律是以完全符合的精確度與小數位數擷取為字串。 如果任何值小於 1，則會遺漏前置零。 money 和 smallmoney 欄位也是如此，因為其為小數位數固定為 4 的 decimal 欄位。

## <a name="add-leading-zeroes-if-missing"></a>若遺漏前置零則加以新增
從 5.6.0 版開始，連線或陳述式屬性 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 允許使用者對小數字串進行格式設定。 此屬性預期的是布林值 (true 或 false)，且只影響所擷取結果中 decimal 或 numeric 值的格式設定。 換句話說，此屬性不影響插入或更新等其他作業。

根據預設，`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 是 **false**。 如果設定為 true，則會將十進位字串的前置零新增至小於 1 的任何十進位值。

## <a name="configure-number-of-decimal-places"></a>設定小數位數的數目
當 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 開啟時，另一個連接或陳述式屬性 (`PDO::SQLSRV_ATTR_DECIMAL_PLACES`) 可讓使用者設定顯示 money 和 smallmoney 資料時的小數位數數目。 其接受範圍在 [0, 4] 內的整數值，而在顯示時可能會發生進位。 不過，底層 money 資料會維持不變。

陳述式屬性一律會覆寫對應的連線設定。 請注意，`PDO::SQLSRV_ATTR_DECIMAL_PLACES` 選項**只會**影響 money 資料，且 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 必須設定為 true。 否則，不論 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 設定為何，格式設定都會關閉。

> [!NOTE]
> 因為 money 或 smallmoney 欄位的小數位數為 4，所以將 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 設定為任何負數或大於 4 的任何值，都會被忽略。 不建議使用任何已設定格式的 money 資料作為任何計算的輸入。

### <a name="to-set-the-connection-attributes"></a>設定連接屬性

-   在連線時設定屬性：

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   在連線後設定屬性：

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>範例 - 設定 money 資料的格式
下列範例顯示如何使用 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) 擷取 money 資料：

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>範例 - 覆寫連接屬性
下列範例顯示如何覆寫連接屬性：

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>另請參閱
[將十進位字串及貨幣值格式化 (SQLSRV 驅動程式)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[擷取資料](../../connect/php/retrieving-data.md)
