---
title: 'Pdostatement:: Errorinfo |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1fc81be8628145c63a3d9c2296846ca19b0cc39b
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605618"
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
  
## <a name="remarks"></a>Remarks  
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

[PDO](https://php.net/manual/book.pdo.php)  
  
