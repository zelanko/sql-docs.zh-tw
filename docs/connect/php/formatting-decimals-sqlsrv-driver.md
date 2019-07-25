---
title: 將十進位字串及貨幣值格式化 (SQLSRV 驅動程式) | Microsoft Docs
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
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265138"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>將十進位字串及貨幣值格式化 (SQLSRV 驅動程式)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

為了保留精確度, [decimal 或 numeric 類型](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql)一律會以具有精確精確度和縮放比例的字串形式提取。 如果任何值小於 1, 則會遺漏前置零。 這與 money 和 smallmoney 欄位相同, 因為它們是具有固定小數位數等於4的十進位欄位。

## <a name="add-leading-zeroes-if-missing"></a>如果遺漏, 請新增前置零
從版本5.6.0 版開始, 選項`FormatDecimals`會加入至 sqlsrv 連接和語句層級, 讓使用者能夠格式化十進位字串。 此選項必須要有布林值 (true 或 false), 而且只會影響提取結果中的十進位或數值格式。 換句話說, `FormatDecimals`選項不會影響插入或更新等其他作業。

根據預設，`FormatDecimals` 是 **false**。 如果設定為 true, 則會針對小於1的任何十進位值, 加入前置的零到十進位字串。

## <a name="configure-number-of-decimal-places"></a>設定小數位數
開啟時, 另一個`DecimalPlaces`選項, 可讓使用者設定顯示 money 和 smallmoney 資料時的小數位數。 `FormatDecimals` 它接受 [0, 4] 範圍內的整數值, 而在顯示時可能會發生舍入。 不過, 基礎 money 資料會維持不變。

這兩個選項都可以設定為連接或語句層級, 而語句設定一律會覆寫對應的連接設定。 請注意`DecimalPlaces` , `FormatDecimals`  選項只會影響money資料,而且必須設定為`DecimalPlaces` true, 才會生效。  否則, 無論`DecimalPlaces`設定為何, 都會關閉格式設定。

> [!NOTE]
> 因為 money 或 smallmoney 欄位具有小數位數 4 `DecimalPlaces` , 所以將值設為任何負數或大於4的任何值將會被忽略。 不建議使用任何格式化的 money 資料做為任何計算的輸入。

## <a name="example---a-simple-fetch"></a>範例-簡單的 fetch
下列範例顯示如何在簡單的提取中使用新的選項。

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

## <a name="example---format-the-output-parameter"></a>範例-格式化輸出參數
如果 decimal 或 numeric 欄位當做[output 參數](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)傳回, 傳回的值將會被視為一般 Varchar 字串。 不過, 如果指定了 SQLSRV_SQLTYPE_DECIMAL 或 SQLSRV_SQLTYPE_NUMERIC, 您可以將設定`FormatDecimals`為 true, 以確保數值字串值沒有遺漏前置零。 如需詳細資訊，請參閱[如何：使用 SQLSRV 驅動程式擷取輸出參數](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)。

下列範例顯示如何格式化傳回 decimal (8, 4) 值之預存程式的 output 參數。

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
