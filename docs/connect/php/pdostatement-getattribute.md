---
title: "PDOStatement::getAttribute |Microsoft 文件"
ms.custom: 
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef6cddea6637104695435db5ba429d08faf38050
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取預先定義的 PDOStatement 屬性或自訂驅動程式屬性的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>參數  
$*屬性*： 整數，其中 PDO::ATTR_ * 或 pdo:: SQLSRV_ATTR_\*常數。 支援的屬性是您可以設定的屬性[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)，pdo:: SQLSRV_ATTR_DIRECT_QUERY (如需詳細資訊，請參閱[的直接陳述式執行和已備妥陳述式執行中PDO_SQLSRV 驅動程式](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md))，pdo:: ATTR_CURSOR 和 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE (如需詳細資訊，請參閱[資料指標類型 （PDO_SQLSRV 驅動程式）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md))。  
  
## <a name="return-value"></a>傳回值  
如果成功，會傳回預先定義的 PDO 屬性或自訂驅動程式屬性的 (混合) 值。 如果失敗，則傳回 Null。  
  
## <a name="remarks"></a>備註  
如需範例，請參閱 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

