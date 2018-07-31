---
title: 'Pdo:: prepare |Microsoft Docs'
ms.custom: ''
ms.date: 07/10/2017
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
ms.openlocfilehash: 717657cabc469488565985e3e37d111bb9d592b8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979763"
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
|PDO::ATTR_EMULATE_PREPARES|當 pdo:: ATTR_EMULATE_PREPARES 開啟時，繫結參數取代的已備妥的陳述式中的預留位置。 完整的 SQL 陳述式與任何預留位置然後傳送至是在資料庫中。 <br /><br />Pdo:: ATTR_EMULATE_PREPARES 可用來略過 SQL Server 中的某些限制。 例如，SQL Server 不支援某些 TRANSACT-SQL 子句中具名或位置參數。 此外，SQL Server 的繫結 2100年參數的上限。<br /><br />您可以將 pdo:: ATTR_EMULATE_PREPARES 屬性為 true。 例如：<br /><br />`PDO::ATTR_EMULATE_PREPARES => true`<br /><br />根據預設，此屬性設為 false。<br /><br />**注意** ：當您使用 `PDO::ATTR_EMULATE_PREPARES => true`時，參數化查詢的安全性將沒有效用。 您的應用程式應確定繫結至參數的資料並不包含惡意 Transact-SQL 程式碼。<br /><br />**限制：**： 因為參數未繫結使用資料庫的參數化的查詢功能，不支援 input_output 和輸出參數。|  
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
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
