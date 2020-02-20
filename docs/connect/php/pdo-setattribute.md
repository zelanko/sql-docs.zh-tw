---
title: PDO::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80a3f907e4606201255d0442d136f77c9b31dd40
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76940460"
---
# <a name="pdosetattribute"></a>PDO::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

設定預先定義的 PDO 屬性或自訂的驅動程式屬性。  
  
## <a name="syntax"></a>語法  
  
```
bool PDO::setAttribute ( $attribute, $value );  
```  
  
#### <a name="parameters"></a>參數  
*$attribute*：要設定的屬性。 如需支援的屬性清單，請參閱「備註」一節。  
  
*$value*：值 (混合類型)。  
  
## <a name="return-value"></a>傳回值  
如果成功則傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>備註  
  
|屬性|處理者|支援的值|描述|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|指定資料行名稱的大小寫。<br /><br />PDO::CASE_LOWER 會產生小寫的資料行名稱。<br /><br />PDO::CASE_NATURAL (預設值) 會顯示資料庫所傳回的資料行名稱。<br /><br />PDO::CASE_UPPER 會使資料行名稱以大寫顯示。<br /><br />此屬性可以使用 PDO::setAttribute 來設定。|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|請參閱 PDO 文件。|請參閱 PDO 文件。|  
|PDO::ATTR_DEFAULT_STR_PARAM|PDO|PDO::PARAM_STR_CHAR<br /><br />PDO::PARAM_STR_NATL|如需詳細資訊，請參閱 [PDO::quote](../../connect/php/pdo-quote.md) 中的範例。|
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|指定驅動程式報告失敗的方式。<br /><br />PDO::ERRMODE_SILENT (預設值) 會設定錯誤碼和資訊。<br /><br />PDO::ERRMODE_WARNING 會引發 E_WARNING。<br /><br />PDO::ERRMODE_EXCEPTION 會擲回例外狀況。<br /><br />此屬性可以使用 PDO::setAttribute 來設定。|  
|PDO::ATTR_ORACLE_NULLS|PDO|請參閱 PDO 文件。|指定應如何傳回 Null。<br /><br />PDO::NULL_NATURAL 不會執行任何轉換。<br /><br />PDO::NULL_EMPTY_STRING 會將空字串轉換為 Null。<br /><br />PDO::NULL_TO_STRING 會將 Null 轉換為空字串。|  
|PDO::ATTR_STATEMENT_CLASS|PDO|請參閱 PDO 文件。|設定衍生自 PDOStatement 的使用者提供陳述式類別。<br /><br />需要 `array(string classname, array(mixed constructor_args))`。<br /><br />如需詳細資訊，請參閱 PDO 文件。|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true 或 false|在擷取資料時，將數值轉換為字串。|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 到 PHP 記憶體限制。|設定使用用戶端資料指標時，將保留結果集的緩衝區大小。<br /><br />如果未在 php.ini 檔案中指定，則預設值為 10240 KB。<br /><br />不允許使用零和負數。<br /><br />如需建立用戶端資料指標之查詢的詳細資訊，請參閱[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|介於 0 和 4 (含) 之間的整數|指定將擷取的貨幣值格式化時的小數位數。<br /><br />將忽略任何大於 4 的負整數或值。<br /><br />此選項只有在 PDO::SQLSRV_ATTR_FORMAT_DECIMALS 為 true 時適用。<br /><br />此選項也可在陳述式層級設定。 如果是，則陳述式層級選項會覆寫此選項。<br /><br />如需詳細資訊，請參閱[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 或 false|指定直接或備妥的查詢執行。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|設定驅動程式用來與伺服器通訊的字元集編碼。<br /><br />不支援 PDO::SQLSRV_ENCODING_BINARY。<br /><br />預設值為 PDO::SQLSRV_ENCODING_UTF8。|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 或 false|指定是否要以 [PHP DateTime](http://php.net/manual/en/class.datetime.php) \(英文\) 物件形式擷取日期和時間類型。 如果保留 false，則預設行為是以字串形式傳回它們。<br /><br />此選項也可在陳述式層級設定。 如果是，則陳述式層級選項會覆寫此選項。<br /><br />如需詳細資訊，請參閱[如何：使用 PDO_SQLSRV 驅動程式以 PHP DateTime 物件形式擷取日期和時間類型](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 或 false|處理從數值 SQL 類型 (bit、integer、smallint、tinyint、float 及 real) 資料行擷取的數值。<br /><br />開啟連線選項旗標 ATTR_STRINGIFY_FETCHES 時，即使已開啟 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE，傳回的值還是字串。<br /><br />若繫結資料行中傳回的 PDO 類型為 PDO_PARAM_INT，即使已關閉 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE，整數資料行的傳回值還是 int。|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 或 false|指定是否要在適當時於十進位字串中新增前置零。 如果設定，此選項就會啟用 PDO::SQLSRV_ATTR_DECIMAL_PLACES 選項來將貨幣類型格式化。 如果保留 False，則使用傳回精確的有效位數，並針對小於 1 的值省略前置零的預設行為。<br /><br />此選項也可在陳述式層級設定。 如果是，則陳述式層級選項會覆寫此選項。<br /><br />如需詳細資訊，請參閱[將十進位字串及貨幣值格式化 (PDO_SQLSRV 驅動程式)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)。| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|設定查詢逾時 (以秒為單位)。<br /><br />預設值為 0，表示驅動程式將會無限期地等候結果。<br /><br />不允許使用負數。|  
  
PDO 會處理一些預先定義的屬性，且需要驅動程式才能處理其他屬性。 驅動程式會處理所有的自訂屬性和連接選項。 不支援的屬性、連線選項或不支援的值會根據 PDO::ATTR_ERRMODE 的設定來報告。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例說明如何設定 PDO::ATTR_ERRMODE 屬性。  
  
```  
<?php  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
  
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
