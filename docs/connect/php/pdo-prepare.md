---
title: PDO::prepare | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8765718829f3df3bca5fd289ec326f9d7aad861
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919198"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

進行執行陳述式的準備。

## <a name="syntax"></a>語法

```
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )
```

#### <a name="parameters"></a>參數
$*statement*：一個包含 SQL 陳述式的字串。

*key_pair*：包含屬性名稱和值的陣列。 如需詳細資訊，請參閱「備註」一節。

## <a name="return-value"></a>傳回值
如果成功，則傳回 PDOStatement 物件。 如果失敗，則會根據 `PDO::ATTR_ERRMODE` 的值傳回 PDOException 物件或 false。

## <a name="remarks"></a>備註
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 在執行之前不會評估備妥的陳述式。

下表列出可能的 *key_pair* 值。

|Key|描述|
|-------|---------------|
|PDO::ATTR_CURSOR|指定資料指標行為。 預設值為 `PDO::CURSOR_FWDONLY`，此為不可捲動的順向資料指標。 `PDO::CURSOR_SCROLL` 為可捲動的資料指標。<br /><br />例如： `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )` 。<br /><br />設定為 `PDO::CURSOR_SCROLL` 時，您接著可以使用 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` 來設定可捲動資料指標類型，如下所述。<br /><br />如需 PDO_SQLSRV 驅動程式中的結果集和資料指標的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|
|PDO::ATTR_EMULATE_PREPARES|根據預設，此屬性為 false，您可以使用這個 `PDO::ATTR_EMULATE_PREPARES => true` 進行變更。 如需詳細資訊和範例，請參閱[模擬準備](#emulate-prepare)。|
|PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE|指定可捲動資料指標的類型。 只有在將 `PDO::ATTR_CURSOR` 設定為 `PDO::CURSOR_SCROLL` 時有效。 如需此屬性可接受的值，請參閱下方內容。|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|指定將擷取的貨幣值格式化時的小數位數。 此選項只有當 `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` 為 true 時才能運作。 如需詳細資訊，請參閱[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|若為 True，將會指定直接查詢執行。 False 表示備妥的陳述式執行。 如需 `PDO::SQLSRV_ATTR_DIRECT_QUERY` 的詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (預設值)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|指定是否要以 [PHP DateTime](http://php.net/manual/en/class.datetime.php) \(英文\) 物件形式擷取日期和時間類型。 如需詳細資訊，請參閱[操作說明：使用 PDO_SQLSRV 驅動程式以 PHP DateTime 物件形式擷取日期和時間類型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|處理從數值 SQL 類型資料行擷取的數值。 如需詳細資訊，請參閱 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)。|
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|指定是否要在適當時於十進位字串中新增前置零。 如果設定，此選項就會啟用 `PDO::SQLSRV_ATTR_DECIMAL_PLACES` 選項來將貨幣類型格式化。 如需詳細資訊，請參閱[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|如需詳細資訊，請參閱 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)。|

使用 `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` 時，您可以使用 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` 來指定資料指標的類型。 例如，將下列陣列傳遞至 PDO::prepare 來設定動態資料指標：
```
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));
```
下表會顯示 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` 的可能值。 如需可捲動資料指標的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。

|值|描述|
|---------|---------------|
|PDO::SQLSRV_CURSOR_BUFFERED|建立用戶端 (已緩衝處理) 的靜態資料指標，其會在用戶端電腦上的記憶體中緩衝處理結果集。|
|PDO::SQLSRV_CURSOR_DYNAMIC|建立伺服器端 (無緩衝) 動態資料指標，它可讓您以任何順序存取資料列，且會反映資料庫中的變更。|
|PDO::SQLSRV_CURSOR_KEYSET|建立伺服器端索引鍵集資料指標。 如果資料列已從資料表中刪除，則索引鍵集資料指標不會更新資料列計數 (已刪除的資料列傳回時不會有值)。|
|PDO::SQLSRV_CURSOR_STATIC|建立伺服器端靜態資料指標，它可讓您以任何順序存取資料列，但將不會反映資料庫中的變更。<br /><br />`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` 意指 `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC`。|

您可以呼叫 `unset` 來關閉 PDOStatement 物件：
```
unset($stmt);
```

## <a name="example"></a>範例
此範例示範如何搭配參數標記和順向資料指標來使用 PDO::prepare。

```
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$col1 = 'a';
$col2 = 'b';

$query = "insert into Table1(col1, col2) values(?, ?)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( $col1, $col2 ) );
print $stmt->rowCount();
echo "\n";

$query = "insert into Table1(col1, col2) values(:col1, :col2)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );
print $stmt->rowCount();

unset($stmt);
?>
```

## <a name="example"></a>範例
此範例示範如何搭配伺服器端靜態資料指標來使用 PDO::prepare。 如需示範用戶端資料指標的範例，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。

```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
$stmt->execute();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

## <a name="example"></a>範例
下列兩個程式碼片段會顯示如何搭配以 CHAR/VARCHAR 資料行為目標的資料使用 PDO::prepare。 由於 PDO::prepare 的預設編碼為 UTF-8，使用者可以使用 `PDO::SQLSRV_ENCODING_SYSTEM` 選項來避免隱含轉換。

**選項 1**
```
$options = array(PDO::SQLSRV_ATTR_ENCODING => PDO::SQLSRV_ENCODING_SYSTEM);
$statement = $pdo->prepare(
  'SELECT *
   FROM myTable
   WHERE myVarcharColumn = :myVarcharValue',
  $options
);

$statement->bindValue(':myVarcharValue', 'my data', PDO::PARAM_STR);
```

**選項 2**
```
$statement = $pdo->prepare(
  'SELECT *
   FROM myTable
   WHERE myVarcharColumn = :myVarcharValue'
);
$p = 'my data';
$statement->bindParam(':myVarcharValue', $p, PDO::PARAM_STR, 0, PDO::SQLSRV_ENCODING_SYSTEM);
```

<a name="emulate-prepare" />

## <a name="example"></a>範例

此範例示範如何搭配設定為 true 的 `PDO::ATTR_EMULATE_PREPARES` 來使用 PDO::prepare。

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$database = "tempdb";
$conn = new PDO("sqlsrv:server = $serverName; Database = $database", $username, $password);

$pdo_options = array();
$pdo_options[PDO::ATTR_EMULATE_PREPARES] = true;
$pdo_options[PDO::SQLSRV_ATTR_ENCODING] = PDO::SQLSRV_ENCODING_UTF8;

$stmt = $conn->prepare("CREATE TABLE TEST([id] [int] IDENTITY(1,1) NOT NULL,
                                          [name] nvarchar(max))",
                                          $pdo_options);
$stmt->execute();

$prefix = '가각';
$name = '가각ácasa';
$name2 = '가각sample2';

$stmt = $conn->prepare("INSERT INTO TEST(name) VALUES(:p0)", $pdo_options);
$stmt->execute(['p0' => $name]);
unset($stmt);

$stmt = $conn->prepare("SELECT * FROM TEST WHERE NAME LIKE :p0", $pdo_options);
$stmt->execute(['p0' => "$prefix%"]);
foreach ($stmt as $row) {
    echo "\n" . 'FOUND: ' . $row['name'];
}

unset($stmt);
unset($conn);
?>
```

PDO_SQLSRV 驅動程式會在內部使用 [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md) 所繫結的參數來取代所有預留位置。 因此，會將不含任何預留位置的 SQL 查詢字串傳送至伺服器。 請考量此範例，

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

藉由將 `PDO::ATTR_EMULATE_PREPARES` 設定為 false (預設情況)，傳送至資料庫的資料為：

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

伺服器將使用其用於繫結參數的參數化查詢功能來執行查詢。 另一方面，藉由將 `PDO::ATTR_EMULATE_PREPARES` 設定為 true，傳送至伺服器的查詢本質上為：

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

將 `PDO::ATTR_EMULATE_PREPARES` 設定為 true，可以略過 SQL Server 中的一些限制。 例如，SQL Server 不支援某些 Transact-SQL 子句中的具名或位置參數。 此外，SQL Server 具有繫結 2100 個參數的上限。

> [!NOTE]
> 若將模擬準備設定為 true，參數化查詢的安全性就沒有任何作用。 所以，您的應用程式應確定繫結至參數的資料並不包含惡意 Transact-SQL 程式碼。

### <a name="encoding"></a>編碼

如果使用者想要繫結含不同編碼 (例如 UTF-8 或二進位) 的參數，則使用者應該明確地在 PHP 指令碼中指定編碼。

PDO_SQLSRV 驅動程式會先檢查 `PDO::bindParam()` 中指定的編碼 (例如 `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`)。

如果找不到，驅動程式就會檢查是否已在 `PDO::prepare()` 或 `PDOStatement::setAttribute()` 中設定任何編碼。 否則，此驅動程式將使用 `PDO::__construct()` 或 `PDO::setAttribute()` 中所指定的編碼。

此外，從 5.8.0 版開始，搭配將 `PDO::ATTR_EMULATE_PREPARES` 設定為 true 來使用 PDO::prepare 時，使用者可以使用[在 PHP 7.2 中引進的擴充字串類型](https://wiki.php.net/rfc/extended-string-types-for-pdo) \(英文\) 來確保會使用 `N` 前置詞。 下列程式碼片段會顯示各種替代方案。

> [!NOTE]
> 根據預設，emulate prepares 會設定為 false；在該情況下，系統將會忽略擴充的 PDO 字串常數。

**繫結時使用驅動程式選項 PDO::SQLSRV_ENCODING_UTF8**

```
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true);
$stmt = $conn->prepare($sql, $options);
$stmt->bindParam(':value', $p, PDO::PARAM_STR, 0, PDO::SQLSRV_ENCODING_UTF8);
$stmt->execute();
```

**使用 PDO::SQLSRV_ATTR_ENCODING 屬性**

```
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true, PDO::SQLSRV_ATTR_ENCODING => PDO::SQLSRV_ENCODING_UTF8);
$stmt = $conn->prepare($sql, $options);
$stmt->execute([':value' => $p]);
```

**使用 PDO 常數 PDO::PARAM_STR_NATL**
```
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true);
$stmt = $conn->prepare($sql, $options);
$stmt->bindParam(':value', $p, PDO::PARAM_STR | PDO::PARAM_STR_NATL);
$stmt->execute();
```

**設定預設字串參數類型 PDO::PARAM_STR_NATL**
```
$conn->setAttribute(PDO::ATTR_DEFAULT_STR_PARAM, PDO::PARAM_STR_NATL);
$p = '가각';
$sql = 'SELECT :value';
$options = array(PDO::ATTR_EMULATE_PREPARES => true);
$stmt = $conn->prepare($sql, $options);
$stmt->execute([':value' => $p]);
```

### <a name="limitations"></a>限制

如您所見，繫結會在內部由驅動程式來完成。 有效的查詢會在不含任何參數的情況下傳送到伺服器來執行。 相較於一般情況，會在未使用參數化查詢功能時產生一些限制。

- 不適用繫結為 `PDO::PARAM_INPUT_OUTPUT` 的參數。
    - 當使用者在 `PDO::PARAM_INPUT_OUTPUT` 中指定 `PDO::bindParam()` 時，即會擲回 PDO 例外狀況。
- 它不適用繫結為輸出參數的參數。
    - 當使用者搭配用來作為輸出參數的預留位置 (也就是，在預留位置後面緊接著等號，例如 `SELECT ? = COUNT(*) FROM Table1`) 建立已備妥的陳述式時，即會擲回 PDO 例外狀況。
    - 當已備妥的陳述式使用預留位置作為輸出參數的引數來叫用預存程序時，不會擲回任何例外狀況，因為驅動程式無法偵測到該輸出參數。 不過，使用者針對輸出參數提供的變數將維持不變。
- 對於二進位編碼參數的重複預留位置將無法運作。

## <a name="see-also"></a>另請參閱
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)

