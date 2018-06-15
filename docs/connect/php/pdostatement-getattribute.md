---
title: PDOStatement::getAttribute |Microsoft 文件
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2c02170c88066ed30b99fb1fca46505b099752f
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308507"
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

[PDO](http://php.net/manual/book.pdo.php)  
  
