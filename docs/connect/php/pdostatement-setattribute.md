---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fba09d6c9e9e3b9806943802466628f820bece8f
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

設定屬性值，可以是預先定義的 PDO 屬性，或自訂的驅動程式屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>參數  
$*屬性*： 整數，其中 PDO::ATTR_ * 或 pdo:: SQLSRV_ATTR_\*常數。 如需可用屬性清單，請參閱「備註」一節。  
  
$*值*: （混合） 的值設定為指定的 $*屬性*。  
  
## <a name="return-value"></a>傳回值  
成功時傳回 TRUE，否則傳回 FALSE。  
  
## <a name="remarks"></a>備註  
下表包含可用屬性清單：  
  
|attribute|值|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 到 PHP 記憶體限制。|設定將保留用戶端資料指標結果集的緩衝區大小。<br /><br />預設值為 10240 KB (10 MB)。<br /><br />如需用戶端資料指標的詳細資訊，請參閱[資料指標類型&#40;PDO_SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)。|  
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (預設值)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|設定驅動程式用來與伺服器通訊的字元集編碼。|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true 或 false|處理數值擷取資料行和數值 SQL 型別 （位元、 整數、 smallint、 tinyint、 float、 或真實）。<br /><br />連線選項旗標 ATTR_STRINGIFY_FETCHES 時，傳回值會是字串，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 上。<br /><br />PDO_PARAM_INT 繫結資料行中傳回的 PDO 型別時，整數資料行的傳回值會是 int，即使 SQLSRV_ATTR_FETCHES_NUMERIC_TYPE 已關閉。|  
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

[PDO](http://php.net/manual/book.pdo.php)  
  
