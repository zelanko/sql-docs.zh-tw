---
title: PDOStatement::errorCode
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中的 PDOStatement::errorCode 函式適用的 API 參考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4161abec-c12b-444e-9de5-f1dac7b3e0e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a514d18bc03d1cbbc05b3e75f98e93a88535c9e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645219"
---
# <a name="pdostatementerrorcode"></a>PDOStatement::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

擷取資料庫陳述式物件上最新作業的 SQLSTATE。  
  
## <a name="syntax"></a>語法  
  
```  
  
string PDOStatement::errorCode();  
```  
  
## <a name="return-value"></a>傳回值  
以字串形式傳回五字元的 SQLSTATE；如果沒有陳述式控制代碼的作業，則傳回 NULL。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例說明具有錯誤的 SQL 查詢。  這時會顯示錯誤碼。  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print $stmt->errorCode();  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDOStatement 類別](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
