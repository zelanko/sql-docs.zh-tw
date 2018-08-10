---
title: 'Pdo:: prepare |Microsoft Docs'
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ac27dbcc186eff263803da714032d532c95d3b4
ms.sourcegitcommit: f9d4f9c1815cff1689a68debdccff5e7ff97ccaf
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/31/2018
ms.locfileid: "39367700"
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
如果成功，則傳回 PDOStatement 物件。 如果失敗，則傳回 PDOException 物件或 false，視 PDO::ATTR_ERRMODE 的值而定。  
  
## <a name="remarks"></a>Remarks  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 在執行之前不會評估備妥的陳述式。  
  
下表列出可能的 *key_pair* 值。  
  
|索引鍵|Description|  
|-------|---------------|  
|PDO::ATTR_CURSOR|指定資料指標行為。 預設值為 PDO::CURSOR_FWDONLY。 PDO::CURSOR_SCROLL 是靜態資料指標。<br /><br />例如， `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`。<br /><br />如果您使用 PDO::CURSOR_SCROLL，則可以使用 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE，其說明如下。<br /><br />如需 PDO_SQLSRV 驅動程式中的結果集和資料指標的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::ATTR_EMULATE_PREPARES|根據預設，此屬性為 false，其可以變更這個`PDO::ATTR_EMULATE_PREPARES => true`。 請參閱[模擬準備](#emulate-prepare)如需詳細資訊和範例。|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (預設值)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|若為 True，將會指定直接查詢執行。 False 表示備妥的陳述式執行。 如需 PDO::SQLSRV_ATTR_DIRECT_QUERY 的詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|如需詳細資訊，請參閱 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)。|  
  
當您使用 PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL 時，您可以使用 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE。 例如，  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
下表顯示可能的 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE 值。  
  
|ReplTest1|Description|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|建立用戶端 (緩衝) 靜態資料指標。 如需用戶端資料指標的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_CURSOR_DYNAMIC|建立伺服器端 (無緩衝) 動態資料指標，它可讓您以任何順序存取資料列，且會反映資料庫中的變更。|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|建立伺服器端索引鍵集資料指標。 如果資料列已從資料表中刪除，則索引鍵集資料指標不會更新資料列計數 (已刪除的資料列傳回時不會有值)。|  
|PDO::SQLSRV_CURSOR_STATIC|建立伺服器端靜態資料指標，它可讓您以任何順序存取資料列，但將不會反映資料庫中的變更。<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL 意味著 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC。|  
  
將 PDOStatement 物件設定為 null，即可關閉該物件。  
  
## <a name="example"></a>範例  
此範例說明如何使用具有參數標記和順向資料指標的 PDO::prepare 方法。  
  
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
  
$stmt = null  
?>  
```  

## <a name="example"></a>範例  
此範例說明如何使用具有用戶端資料指標的 PDO::prepare 方法。 如需說明伺服器端資料指標的範例，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。  
  
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

<a name="emulate-prepare" />

## <a name="example"></a>範例 

此範例示範如何使用 pdo:: prepare 方法加`PDO::ATTR_EMULATE_PREPARES`設為 true。 

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

PDO_SQLSRV 驅動程式在內部使用由繫結的參數取代所有預留位置[PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md)。 因此，任何預留位置以 SQL 查詢字串傳送至伺服器。 請考慮這個範例中，

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

使用`PDO::ATTR_EMULATE_PREPARES`設為 false （預設情況下），傳送至資料庫的資料是：

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

伺服器會執行查詢使用其參數型的查詢功能的繫結參數。 相反地，使用`PDO::ATTR_EMULATE_PREPARES`本質上是設為 true，傳送至伺服器的查詢：

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

設定`PDO::ATTR_EMULATE_PREPARES`以 true 可以略過 SQL Server 中的一些限制。 例如，SQL Server 不支援某些 TRANSACT-SQL 子句中具名或位置參數。 此外，SQL Server 的繫結 2100年參數的上限。

> [!NOTE]
> Emulate 準備設為 true，參數化查詢的安全性將沒有作用中。 所以，您的應用程式應確定繫結至參數的資料並不包含惡意 Transact-SQL 程式碼。

### <a name="encoding"></a>編碼方式

如果使用者想要使用不同的編碼 （例如 utf-8 或二進位） 的參數繫結，使用者應該清楚地指定在 PHP 指令碼中的編碼方式。

PDO_SQLSRV 驅動程式會先檢查中指定的編碼`PDO::bindParam()`(例如`$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`)。 

如果找不到驅動程式會檢查任何編碼中設時`PDO::prepare()`或`PDOStatement::setAttribute()`。 否則，此驅動程式將使用中指定的編碼`PDO::__construct()`或`PDO::setAttribute()`。

### <a name="limitations"></a>限制

如您所見，繫結是在內部由驅動程式。 有效的查詢傳送到伺服器上，執行不含任何參數。 相較於一般的情況下，參數化的查詢功能不在使用時產生一些限制。

- 不適用於參數的繫結為`PDO::PARAM_INPUT_OUTPUT`。
    - 當使用者指定`PDO::PARAM_INPUT_OUTPUT`在`PDO::bindParam()`，PDO 例外狀況。
- 不適用於繫結為輸出參數的參數之用。
    - 當使用者已備妥的陳述式以建立預留位置，供輸出參數 (也就是有等號後面的預留位置，例如`SELECT ? = COUNT(*) FROM Table1`)，PDO 例外狀況。
    - 當已備妥的陳述式中，會叫用具有預留位置的預存程序當做輸出參數的引數時，因為驅動程式無法偵測到的輸出參數，會擲不回任何例外狀況。 不過，使用者會提供輸出參數的變數會維持不變。
- 重複的二進位編碼的參數預留位置將無法運作

## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
