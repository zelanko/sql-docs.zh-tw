---
title: 'Pdo:: query |Microsoft 文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb23a63d77461cb13784c515bd0638af277e63b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

執行 SQL 查詢並以 PDOStatement 物件形式傳回結果集。  
  
## <a name="syntax"></a>語法  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>參數  
*$statement*：您要執行的 SQL 陳述式。  
  
*$fetch_style*： 有關如何執行查詢的選擇性指示。 如需詳細資訊，請參閱＜備註＞一節。 $*fetch_style* pdo:: query 會覆寫以 $*fetch_style* pdo:: fetch 中。  
  
## <a name="return-value"></a>傳回值  
如果呼叫成功，PDO::query 會傳回 PDOStatement 物件。 如果呼叫失敗，PDO::query 會擲回 PDOException 物件或傳回 false (視 PDO::ATTR_ERRMODE 的設定而定)。  
  
## <a name="exceptions"></a>例外狀況  
PDOException。  
  
## <a name="remarks"></a>備註  
使用 pdo:: query 執行的查詢可以執行已備妥的陳述式或直接根據 pdo:: SQLSRV_ATTR_DIRECT_QUERY 的設定。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式中的直接陳述式執行和已備妥的陳述式執行](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)。  
  
Pdo:: SQLSRV_ATTR_QUERY_TIMEOUT 也會影響 pdo:: exec; 行為如需詳細資訊，請參閱[pdo:: setattribute](../../connect/php/pdo-setattribute.md)。  
  
您可以指定下列選項為 $*fetch_style*。  
  
|style|Description|  
|---------|---------------|  
|Pdo:: FETCH_COLUMN， *num*|指定的資料行中資料的查詢。 資料表中的第一個資料行是資料行 0。|  
|Pdo:: FETCH_CLASS，'*classname*'，陣列 (*引數清單*)|建立類別執行個體並將資料行名稱指派給類別中的屬性。 如果類別建構函式採用一或多個參數，您也可以傳遞 *arglist*。|  
|Pdo:: FETCH_CLASS，'*classname*'|將資料行名稱指派給現有類別中的屬性。|  
  
呼叫 PDOStatement::closeCursor，以便於再次呼叫 PDO::query 之前，釋放與 PDOStatement 物件相關聯的資料庫資源。  
  
將 PDOStatement 物件設定為 null，即可關閉該物件。  
  
如果未擷取結果中的所有資料，則下一次 PDO::query 呼叫不會失敗。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例顯示數個查詢。  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
