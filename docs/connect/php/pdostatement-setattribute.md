---
title: 'Pdostatement:: Setattribute |Microsoft Docs'
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ec2ed7275c3580554c385940c5cef134244ae35
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744338"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

設定屬性值，可以是預先定義的 PDO 屬性，或自訂的驅動程式屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>參數  
$*attribute*：一個整數，是 PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常數的其中一個。 如需可用屬性清單，請參閱「備註」一節。  
  
$*value*：要為指定的 $*attribute* 設定的混合值。  
  
## <a name="return-value"></a>傳回值  
成功時傳回 TRUE，否則傳回 FALSE。  
  
## <a name="remarks"></a>Remarks  
下表包含可用屬性清單：  
  
|attribute|值|描述|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 到 PHP 記憶體限制。|設定將保留用戶端資料指標結果集的緩衝區大小。<br /><br />預設值為 10,240 KB (10 MB)。<br /><br />如需用戶端資料指標的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|介於 0 到 4 （含） 之間的整數|指定格式化時的小數位數提取貨幣值。<br /><br />將忽略任何負整數或值大於 4。<br /><br />此選項僅適用於 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 為 true。<br /><br />此選項也可以設定在連接層級。 如果是的話，這個選項會覆寫連接層級的選項。<br /><br />如需詳細資訊，請參閱 <<c0> [ 格式化為十進位字串和貨幣值 （PDO_SQLSRV 驅動程式）](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (預設值)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|設定驅動程式用來與伺服器通訊的字元集編碼。|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true 或 false|指定是否要擷取日期和時間類型作為[PHP DateTime](http://php.net/manual/en/class.datetime.php)物件。 如果保留，則為 false，預設行為是以字串傳回它們。<br /><br />此選項也可以設定在連接層級。 如果是的話，這個選項會覆寫連接層級的選項。<br /><br />如需詳細資訊，請參閱 <<c0> [ 如何： 擷取日期和時間類型做為 PHP DateTime 物件使用 PDO_SQLSRV 驅動程式](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true 或 false|處理數值擷取從資料行和數值 SQL 型別 （位元、 整數、 smallint、 tinyint、 float、 或即時）。<br /><br />開啟連接選項旗標 ATTR_STRINGIFY_FETCHES 時，傳回的值會是字串，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 上。<br /><br />PDO_PARAM_INT 繫結資料行中傳回的 PDO 型別時，整數資料行的傳回值會是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 已關閉。|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true 或 false|指定是否要加入前置零，以適時的十進位字串。 如果設定這個選項可讓您格式化 money 類型的 PDO::SQLSRV_ATTR_DECIMAL_PLACES 選項。 如果保留，則為 false，則會使用傳回精確的有效位數，並省略前置字元小於 1 的值為零的預設行為。<br /><br />此選項也可以設定在連接層級。 如果是的話，這個選項會覆寫連接層級的選項。<br /><br />如需詳細資訊，請參閱 <<c0> [ 格式化為十進位字串和貨幣值 （PDO_SQLSRV 驅動程式）](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|設定查詢逾時 (以秒為單位)。<br /><br />根據預設，驅動程式將會無限期地等候結果。 不允許使用負數。<br /><br />0 表示無逾時。|  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
