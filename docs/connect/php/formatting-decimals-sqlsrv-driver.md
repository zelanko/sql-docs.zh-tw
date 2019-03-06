---
title: 格式化十進位字串和貨幣值 （SQLSRV 驅動程式） |Microsoft Docs
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
ms.openlocfilehash: 76b6d27acedcfe2ec462a764559237a1a2218f78
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676515"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>格式化十進位字串和貨幣值 （SQLSRV 驅動程式）
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

若要保留精確[decimal 或 numeric 類型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)一律會擷取為確切的有效位數與標尺的字串。 如果任何值小於 1，前置的零遺失。 它是相同的 money 和 smallmoney 欄位為十進位的欄位，固定小數位數等於 4。

## <a name="add-leading-zeroes-if-missing"></a>如果遺失則加入零的前置字元
開頭為 5.6.0 版，選項`FormatDecimals`會新增至 sqlsrv 連接和陳述式層級，可讓使用者設定十進位字串的格式。 這個選項需要布林值 （true 或 false），而且只會影響之格式設定的十進位或數值的值中擷取的結果。 換句話說，`FormatDecimals`選項沒有任何作用，插入或更新等其他作業。

根據預設，`FormatDecimals` 是 **false**。 如果設定為 true，前置的零，以十進位字串將會新增任何十進位值小於 1。

## <a name="configure-number-of-decimal-places"></a>設定小數位的數
具有`FormatDecimals`開啟另一個選項， `DecimalPlaces`，可讓使用者設定的小數位數，顯示 money 和 smallmoney 資料時。 它可接受的範圍內的整數值 [0，4]，並且顯示時捨入可能會發生。 不過，基礎 money 資料保持不變。

這兩個選項可以設定為連線或陳述式層級，並設定一律陳述式會覆寫對應的連接設定。 請注意， `DecimalPlaces`  選項**只**影響 money 資料並`FormatDecimals`必須設定為適用於`DecimalPlaces`才會生效。 否則，格式為關閉狀態不論`DecimalPlaces`設定。

> [!NOTE]
> 由於金額或 smallmoney 欄位有擴展 4，設定`DecimalPlaces`任何負數或大於 4 將會忽略任何值的值。 不建議使用任何格式化的 money 資料做為任何計算的輸入。

## <a name="example---a-simple-fetch"></a>範例-使用簡單的擷取
下列範例示範如何使用簡單的提取中新的選項。

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

## <a name="example---format-the-output-parameter"></a>範例-格式的輸出參數
如果傳回的十進位或數值欄位是[輸出參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)，傳回的值會被視為一般 varchar 字串。 不過，如果指定了 SQLSRV_SQLTYPE_DECIMAL 或 SQLSRV_SQLTYPE_NUMERIC，您可以設定`FormatDecimals`為 true，以確保沒有任何遺漏的前置零的數字的字串值。 如需詳細資訊，請參閱[如何：使用 SQLSRV 驅動程式擷取輸出參數](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。

下列範例顯示如何格式化輸出參數傳回 decimal(8,4) 值的預存程序。

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
[格式化十進位字串和貨幣值 （PDO_SQLSRV 驅動程式）](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[擷取資料](../../connect/php/retrieving-data.md)
