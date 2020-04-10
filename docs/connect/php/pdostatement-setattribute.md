---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5c5c0670ceb9725c04a63a59a09b25cf72c810
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925260"
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
  
## <a name="remarks"></a>備註  
下表包含可用屬性清單：  
  
|屬性|值|描述|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 到 PHP 記憶體限制。|設定將保留用戶端資料指標結果集的緩衝區大小。<br /><br />預設值為 10,240 KB (10 MB)。<br /><br />如需用戶端資料指標的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DATA_CLASSIFICATION|true 或 false|指定是否要在呼叫 [PDOStatement::getColumnMeta](../../connect/php/pdostatement-getcolumnmeta.md) 時擷取資料分類中繼資料。 預設值為 false。|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|介於 0 和 4 (含) 之間的整數|指定將擷取的貨幣值格式化時的小數位數。<br /><br />將忽略任何大於 4 的負整數或值。<br /><br />此選項只有在 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 為 true 時適用。<br /><br />此選項也可在連線層級設定。 如果是，則此選項會覆寫連線層級選項。<br /><br />如需詳細資訊，請參閱[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。|
|PDO::SQLSRV_ATTR_ENCODING|整數<br /><br />PDO::SQLSRV_ENCODING_UTF8 (預設值)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|設定驅動程式用來與伺服器通訊的字元集編碼。|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true 或 false|指定是否要以 [PHP DateTime](http://php.net/manual/en/class.datetime.php) \(英文\) 物件形式擷取日期和時間類型。 如果保留 false，則預設行為是以字串形式傳回它們。<br /><br />此選項也可在連線層級設定。 如果是，則此選項會覆寫連線層級選項。<br /><br />如需詳細資訊，請參閱[操作說明：使用 PDO_SQLSRV 驅動程式以 PHP DateTime 物件形式擷取日期和時間類型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true 或 false|處理從數值 SQL 類型 (bit、integer、smallint、tinyint、float 及 real) 資料行擷取的數值。<br /><br />開啟連線選項旗標 ATTR_STRINGIFY_FETCHES 時，即使已開啟 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE，傳回的值還是字串。<br /><br />若繫結資料行中傳回的 PDO 類型為 PDO_PARAM_INT，即使已關閉 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE，整數資料行的傳回值還是 int。|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true 或 false|指定是否要在適當時於十進位字串中新增前置零。 如果設定，此選項就會啟用 PDO::SQLSRV_ATTR_DECIMAL_PLACES 選項來將貨幣類型格式化。 如果保留 False，則使用傳回精確的有效位數，並針對小於 1 的值省略前置零的預設行為。<br /><br />此選項也可在連線層級設定。 如果是，則此選項會覆寫連線層級選項。<br /><br />如需詳細資訊，請參閱[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|整數|設定查詢逾時 (以秒為單位)。<br /><br />根據預設，驅動程式將會無限期地等候結果。 不允許使用負數。<br /><br />0 表示無逾時。|  
  
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
  
