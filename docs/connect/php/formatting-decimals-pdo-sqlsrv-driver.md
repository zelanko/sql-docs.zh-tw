---
title: 將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式) | Microsoft Docs
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
manager: v-mabarw
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265148"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

為了保留精確度, [decimal 或 numeric 類型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)一律會以具有精確精確度和縮放比例的字串形式提取。 如果任何值小於 1, 則會遺漏前置零。 這與 money 和 smallmoney 欄位相同, 因為它們是具有固定小數位數等於4的十進位欄位。

## <a name="add-leading-zeroes-if-missing"></a>如果遺漏, 請新增前置零
從 version 5.6.0 版開始, connection 或語句屬性`PDO::SQLSRV_ATTR_FORMAT_DECIMALS`可讓使用者格式化十進位字串。 這個屬性必須是布林值 (true 或 false), 而且只會影響提取結果中的十進位或數值格式。 換句話說, 這個屬性不會影響插入或更新等其他作業。

根據預設，`PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 是 **false**。 如果設定為 true, 則會針對小於1的任何十進位值, 加入前置的零到十進位字串。

## <a name="configure-number-of-decimal-places"></a>設定小數位數
在開啟的情況下, 另一個 connection 或`PDO::SQLSRV_ATTR_DECIMAL_PLACES`語句屬性可讓使用者設定顯示 money 和 smallmoney 資料時的小數位數。 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 它接受 [0, 4] 範圍內的整數值, 而在顯示時可能會發生舍入。 不過, 基礎 money 資料會維持不變。

語句屬性一律會覆寫對應的連接設定。 請注意,  `PDO::SQLSRV_ATTR_FORMAT_DECIMALS`選項只會影響 money 資料, 而且必須設定為 true。 `PDO::SQLSRV_ATTR_DECIMAL_PLACES`  否則, 無論`PDO::SQLSRV_ATTR_DECIMAL_PLACES`設定為何, 都會關閉格式設定。

> [!NOTE]
> 由於 money 或 smallmoney 欄位的小數位數為`PDO::SQLSRV_ATTR_DECIMAL_PLACES` 4, 因此將會忽略設定為任何負數或大於4的任何值。 不建議使用任何格式化的 money 資料做為任何計算的輸入。

### <a name="to-set-the-connection-attributes"></a>若要設定連接屬性

-   在連接點設定屬性:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   設定屬性後的連接:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>範例-格式化 money 資料
下列範例顯示如何使用[PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md)提取 money 資料:

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
下列範例顯示如何覆寫連接屬性:

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
