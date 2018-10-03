---
title: PDOStatement::getAttribute |Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17ef88f4dc899ce9108ff4a62cf4bc4bc7f8fabf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738836"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取預先定義的 PDOStatement 屬性或自訂驅動程式屬性的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>參數  
$*attribute*：一個整數，是 PDO::ATTR_* 或 PDO::SQLSRV_ATTR_\* 常數的其中一個。 支援的屬性是您可以使用設定的屬性[pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md)，pdo:: SQLSRV_ATTR_DIRECT_QUERY (如需詳細資訊，請參閱[的直接陳述式執行和已備妥陳述式執行中PDO_SQLSRV 驅動程式](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md))，pdo:: ATTR_CURSOR 和 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE (如需詳細資訊，請參閱 <<c8> [ 資料指標類型 （PDO_SQLSRV 驅動程式）](../../connect/php/cursor-types-pdo-sqlsrv-driver.md))。  
  
## <a name="return-value"></a>傳回值  
如果成功，會傳回預先定義的 PDO 屬性或自訂驅動程式屬性的 (混合) 值。 如果失敗，則傳回 Null。  
  
## <a name="remarks"></a>Remarks  
如需範例，請參閱 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
