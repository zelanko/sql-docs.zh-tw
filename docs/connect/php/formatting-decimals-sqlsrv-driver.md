---
title: 將十進位字串及貨幣值格式化 (SQLSRV 驅動程式)
description: 了解在使用 Microsoft SQLSRV Driver for PHP for SQL Server 時，如何使用 FormatDecimals 和 DecimalPlaces 選項將十進位值或幣值格式化。
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
ms.openlocfilehash: c6d77fb9fcfdc720c4053688f8f0dcf759af15c8
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680723"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>將十進位字串及貨幣值格式化 (SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

為了維持正確性，[decimal 或 numeric 類型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)一律是以完全符合的精確度與小數位數擷取為字串。 如果任何值小於 1，則會遺漏前置零。 money 和 smallmoney 欄位也是如此，因為其為小數位數固定為 4 的 decimal 欄位。

## <a name="add-leading-zeroes-if-missing"></a>若遺漏前置零則加以新增
從 5.6.0 版開始，已將 `FormatDecimals` 選項新增至 sqlsrv 連線和陳述式層級，其可讓使用者格式化十進位字串。 此選項會預期布林值 (true 或 false)，而且只會影響所擷取結果中十進位或數值的格式設定。 換句話說，`FormatDecimals` 選項不會影響插入或更新等其他作業。

根據預設，`FormatDecimals` 是 **false**。 如果設定為 true，則會將十進位字串的前置零新增至小於 1 的任何十進位值。

## <a name="configure-number-of-decimal-places"></a>設定小數位數的數目
當 `FormatDecimals` 開啟時，另一個 `DecimalPlaces` 選項可讓使用者設定顯示 money 和 smallmoney 資料時的小數位數。 其接受範圍在 [0, 4] 內的整數值，而在顯示時可能會發生進位。 不過，底層 money 資料會維持不變。

這兩個選項都可以在連線或陳述式層級設定，且陳述式設定一律會覆寫對應的連線設定。 請注意，`DecimalPlaces` 選項**只會**影響 money 資料，且 `FormatDecimals` 必須設定為 true，`DecimalPlaces` 才會生效。 否則，不論 `DecimalPlaces` 設定為何，格式設定都會關閉。

> [!NOTE]
> 因為 money 或 smallmoney 欄位的小數位數為 4，系統將會忽略將 `DecimalPlaces` 值設定為任何負數或大於 4 的任何值。 不建議使用任何已設定格式的 money 資料作為任何計算的輸入。

## <a name="example---a-simple-fetch"></a>範例 - 簡易擷取
下列範例將示範如何使用新的選項進行簡易擷取。

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>範例 - 格式化輸出參數
如果 decimal 或 numeric 欄位以[輸出參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)的形式傳回，系統會將傳回的值視為一般 varchar 字串。 不過，如果已指定 SQLSRV_SQLTYPE_DECIMAL 或 SQLSRV_SQLTYPE_NUMERIC，您可以將 `FormatDecimals` 設定為 true 以確保數值字串值沒有任何遺失的前置零。 如需詳細資訊，請參閱[如何：使用 SQLSRV 驅動程式擷取輸出參數](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。

下列範例示範如何格式化傳回 decimal(8,4) 值之預存程序的輸出參數。

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>另請參閱
[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[擷取資料](../../connect/php/retrieving-data.md)
