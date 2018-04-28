---
title: 'Pdo:: setattribute |Microsoft 文件'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a94273f371b8ed942b945e836e1e6088187276a7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
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
  
*$value*: （混合類型） 的值。  
  
## <a name="return-value"></a>傳回值  
如果成功則傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>備註  
  
|Attribute|處理者|支援的值|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|指定資料行名稱的大小寫。<br /><br />PDO::CASE_LOWER 會產生小寫的資料行名稱。<br /><br />PDO::CASE_NATURAL (預設值) 會顯示資料庫所傳回的資料行名稱。<br /><br />PDO::CASE_UPPER 會使資料行名稱以大寫顯示。<br /><br />此屬性可以使用 PDO::setAttribute 來設定。|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|請參閱 PDO 文件。|請參閱 PDO 文件。|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|指定驅動程式報告失敗的方式。<br /><br />PDO::ERRMODE_SILENT (預設值) 會設定錯誤碼和資訊。<br /><br />PDO::ERRMODE_WARNING 會引發 E_WARNING。<br /><br />PDO::ERRMODE_EXCEPTION 會擲回例外狀況。<br /><br />此屬性可以使用 PDO::setAttribute 來設定。|  
|PDO::ATTR_ORACLE_NULLS|PDO|請參閱 PDO 文件。|指定應如何傳回 Null。<br /><br />PDO::NULL_NATURAL 不會執行任何轉換。<br /><br />PDO::NULL_EMPTY_STRING 會將空字串轉換為 Null。<br /><br />PDO::NULL_TO_STRING 會將 Null 轉換為空字串。|  
|PDO::ATTR_STATEMENT_CLASS|PDO|請參閱 PDO 文件。|設定衍生自 PDOStatement 的使用者提供陳述式類別。<br /><br />需要 `array(string classname, array(mixed constructor_args))`。<br /><br />如需詳細資訊，請參閱 PDO 文件。|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true 或 false|在擷取資料時，將數值轉換為字串。|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 到 PHP 記憶體限制。|設定將保留結果集的緩衝區大小。<br /><br />預設值為 10240 KB (10 MB)。<br /><br />如需建立用戶端資料指標之查詢的詳細資訊，請參閱[資料指標類型&#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|指定直接或備妥的查詢執行。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|設定驅動程式用來與伺服器通訊的字元集編碼。<br /><br />不支援 PDO::SQLSRV_ENCODING_BINARY。<br /><br />預設值為 PDO::SQLSRV_ENCODING_UTF8。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 或 false|處理數值擷取資料行和數值 SQL 型別 （位元、 整數、 smallint、 tinyint、 float、 或真實）。<br /><br />連線選項旗標 ATTR_STRINGIFY_FETCHES 時，傳回值會是字串，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 上。<br /><br />PDO_PARAM_INT 繫結資料行中傳回的 PDO 型別時，整數資料行的傳回值會是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 已關閉。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|設定查詢逾時 (以秒為單位)。<br /><br />預設值為 0，表示驅動程式將會無限期地等候結果。<br /><br />不允許使用負數。|  
|PDO::SQLSRV_CLIENT_BUFFER_MAX_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|設定查詢緩衝區的大小。<br /><br />預設值為 0，緩衝區大小不受限。<br /><br />不允許使用負數。<br /><br />如需建立用戶端資料指標之查詢的詳細資訊，請參閱[資料指標類型&#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
  
PDO 會處理一些預先定義的屬性，且需要驅動程式才能處理其他屬性。 驅動程式會處理所有的自訂屬性和連接選項。 不支援的屬性、 連接選項或不支援的值會根據 pdo:: ATTR_ERRMODE 的設定報告。  
  
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

[PDO](http://php.net/manual/book.pdo.php)  
  
