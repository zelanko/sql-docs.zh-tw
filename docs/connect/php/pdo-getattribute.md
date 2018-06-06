---
title: 'Pdo:: getattribute |Microsoft 文件'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c81833ea-8b8a-459d-8f24-920098da994d
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56e0fc4e6cf98af6b688fe3752b7b57eda134341
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="pdogetattribute"></a>PDO::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取預先定義的 PDO 或驅動程式屬性值。  
  
## <a name="syntax"></a>語法  
  
```  
  
mixed PDO::getAttribute ( $attribute )  
```  
  
#### <a name="parameters"></a>參數  
*$attribute*：其中一個支援的屬性。 如需支援的屬性清單，請參閱＜備註＞一節。  
  
## <a name="return-value"></a>傳回值  
如果成功，會傳回連接選項、預先定義的 PDO 屬性或自訂驅動程式屬性的值。 如果失敗，則會傳回 null。  
  
## <a name="remarks"></a>備註  
下表包含支援的屬性清單。  
  
|Attribute|處理者|支援的值|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|指定資料行名稱是否應為特定的大小寫。 PDO::CASE_LOWER 會強制使用小寫的資料行名稱、PDO::CASE_NATURAL 會保留資料庫所傳回的資料行名稱，而 PDO::CASE_UPPER 會強制使用大寫的資料行名稱。<br /><br />預設值是 PDO::CASE_NATURAL。<br /><br />也可以使用 PDO::setAttribute 設定此屬性。|  
|PDO::ATTR_CLIENT_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|字串陣列|描述驅動程式和相關程式庫的版本。 傳回具有下列元素的陣列： ODBC 版本 (*MajorVer*。*MinorVer*)， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Native Client DLL 名稱和版本、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 (*MajorVer*。*MinorVer*。*BuildNumber*。*修訂*)|  
|PDO::ATTR_DRIVER_NAME|PDO|字串|一律傳回 "sqlsrv"。|  
|PDO::ATTR_DRIVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|字串|指出[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]版本 (*MajorVer*。*MinorVer*。*BuildNumber*。*修訂*)|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|指定驅動程式處理失敗的方式。<br /><br />PDO::ERRMODE_SILENT (預設值) 會設定錯誤碼和資訊。<br /><br />PDO::ERRMODE_WARNING 會引發 E_WARNING。<br /><br />PDO::ERRMODE_EXCEPTION 會引發例外狀況。<br /><br />也可以使用 PDO::setAttribute 設定此屬性。|  
|PDO::ATTR_ORACLE_NULLS|PDO|請參閱 PDO 文件。|請參閱 PDO 文件。|  
|PDO::ATTR_SERVER_INFO|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|3 個元素的陣列|傳回目前的資料庫、SQL Server 版本和 SQL Server 執行個體。|  
|PDO::ATTR_SERVER_VERSION|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|字串|指出 SQL Server 版本 (*主要*。*次要*。*BuildNumber*)|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|請參閱 PDO 文件。|請參閱 PDO 文件。|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 到 PHP 記憶體限制。|設定將保留用戶端資料指標結果集的緩衝區大小。<br /><br />預設值為 10240 KB (10 MB)。<br /><br />如需用戶端資料指標的詳細資訊，請參閱[資料指標類型&#40;SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|指定直接或備妥的查詢執行。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM|指定驅動程式用來與伺服器通訊的字元集編碼。<br /><br />預設值為 PDO::SQLSRV_ENCODING_UTF8。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true 或 false|處理數值擷取資料行和數值 SQL 型別 （位元、 整數、 smallint、 tinyint、 float、 或真實）。<br /><br />連線選項旗標 ATTR_STRINGIFY_FETCHES 時，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 已開啟，則傳回值是字串。<br /><br />PDO_PARAM_INT 繫結資料行中傳回的 PDO 型別時，整數資料行的傳回值會是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 已關閉。|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|integer|設定查詢逾時 (以秒為單位)。<br /><br />預設值為 0，表示驅動程式將會無限期地等候結果。<br /><br />不允許使用負數。|  

  
PDO 會處理一些預先定義的屬性，然而需要驅動程式才能處理其他屬性。 驅動程式會處理所有的自訂屬性和連接選項，而不支援的屬性或連接選項傳回 null。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例顯示 PDO::ATTR_ERRMODE 屬性的值 (在變更其值之前和之後)。  
  
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
  
// An example using PDO::ATTR_CLIENT_VERSION  
print_r($conn->getAttribute( PDO::ATTR_CLIENT_VERSION ));  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
