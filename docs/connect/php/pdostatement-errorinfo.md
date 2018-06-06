---
title: 'Pdostatement:: Errorinfo |Microsoft 文件'
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
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46c2cda3b7b36d534e02a8a4d3a782e3abd94240
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取陳述式控制代碼上最近作業的延伸錯誤資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
array PDOStatement::errorInfo();  
```  
  
## <a name="return-value"></a>傳回值  
有關陳述式控制代碼上最近作業的錯誤資訊陣列。 此陣列包含下列欄位：  
  
-   SQLSTATE 錯誤碼  
  
-   驅動程式特有的錯誤碼  
  
-   驅動程式特有的錯誤訊息  
  
如果沒有發生錯誤，或如果未設定 SQLSTATE，則驅動程式特有的欄位會是 NULL。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
在此範例中，SQL 陳述式有錯誤，而後會予以報告。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
