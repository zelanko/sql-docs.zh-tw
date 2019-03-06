---
title: 格式化十進位字串和貨幣值 （PDO_SQLSRV 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: mbarwin
ms.openlocfilehash: 35626c192c3d74ad0201cee3c5e97adbce92a3aa
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676529"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>格式化十進位字串和貨幣值 （PDO_SQLSRV 驅動程式）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

若要保留精確[decimal 或 numeric 類型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)一律會擷取為確切的有效位數與標尺的字串。 如果任何值小於 1，前置的零遺失。 它是相同的 money 和 smallmoney 欄位為十進位的欄位，固定小數位數等於 4。

## <a name="add-leading-zeroes-if-missing"></a>如果遺失則加入零的前置字元
開頭為 5.6.0 版、 連線或陳述式屬性`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`可讓使用者設定十進位字串的格式。 這個屬性需要布林值 （true 或 false），而且只會影響擷取的結果中的十進位或數值值的格式。 換句話說，此屬性會有不會影響其他作業，例如插入或更新。

根據預設，`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 是 **false**。 如果設定為 true，前置的零，以十進位字串將會新增任何十進位值小於 1。

## <a name="configure-number-of-decimal-places"></a>設定小數位的數
具有`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`開啟另一個連接或陳述式的屬性， `PDO::SQLSRV_ATTR_DECIMAL_PLACES`，可讓使用者設定的小數位數，顯示 money 和 smallmoney 資料時。 它可接受的範圍內的整數值 [0，4]，並且顯示時捨入可能會發生。 不過，基礎 money 資料保持不變。

陳述式屬性永遠會覆寫對應的連線設定。 請注意， `PDO::SQLSRV_ATTR_DECIMAL_PLACES`  選項**只**影響 money 資料和`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`必須設定為 true。 否則，格式為關閉狀態不論`PDO::SQLSRV_ATTR_DECIMAL_PLACES`設定。

> [!NOTE]
> 由於金額或 smallmoney 欄位有擴展 4，設定`PDO::SQLSRV_ATTR_DECIMAL_PLACES`任何負數或大於 4 將會忽略任何值。 不建議使用任何格式化的 money 資料做為任何計算的輸入。

### <a name="to-set-the-connection-attributes"></a>若要設定的連接屬性

-   在 連接點的設定屬性：

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   設定屬性 post 連線：

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>範例-格式 money 資料
下列範例示範如何擷取 money 資料使用[pdostatement:: Bindcolumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>範例-覆寫連接屬性
下列範例示範如何覆寫連接屬性：

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
[格式化十進位字串和貨幣值 （SQLSRV 驅動程式）](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[擷取資料](../../connect/php/retrieving-data.md)
