---
title: PDOStatement::getColumnMeta |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8211a6a4cda4a5efa29b7379c24ba3fbbfa5458e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37983006"
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取資料行的中繼資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>參數  
*$conn*：(整數) 您要擷取其中繼資料的資料行號碼 (以零起始)。  
  
## <a name="return-value"></a>傳回值  
包含資料行中繼資料的關聯陣列 (索引鍵和值)。 如需陣列中欄位的描述，請參閱＜備註＞一節。  
  
## <a name="remarks"></a>Remarks  
下表將描述 getColumnMeta 所傳回陣列中的欄位。  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|指定資料行的 PHP 類型。 一定是字串。|  
|driver:decl_type|指定用來表示資料庫中的資料行值的 SQL 類型。 如果結果集內的資料行是函數的結果，則此值不是由 PDOStatement::getColumnMeta 傳回。|  
|flags|指定為此資料行設定的旗標。 一律是 0。|  
|NAME|指定資料庫中資料行的名稱。|  
|資料表|指定包含資料庫中資料行的資料表名稱。 永遠為空白。|  
|len|指定資料行長度。|  
|有效位數|指定此資料行的數值有效位數。|  
|pdo_type|指定此資料行的類型 (以 PDO::PARAM_* 常數表示)。 一律是 PDO::PARAM_STR (2)。|  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
