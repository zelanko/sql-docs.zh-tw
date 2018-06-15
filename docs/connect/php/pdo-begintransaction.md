---
title: 'Pdo:: begintransaction |Microsoft 文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48b5d1343a941904280c33f5a983be944c751f2f
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307967"
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

關閉自動認可模式，並開始交易。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>傳回值  
如果方法呼叫成功，會傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>備註  
以 pdo:: begintransaction 開始的交易時結束[pdo:: commit](../../connect/php/pdo-commit.md)或[pdo:: rollback](../../connect/php/pdo-rollback.md)呼叫。  
  
PDO::beginTransaction 不受 PDO::ATTR_AUTOCOMMIT 的值影響 (且不會影響該值)。  
  
在使用 PDO::rollback 或 PDO::commit 結束先前的 PDO::beginTransaction 之前，您無法呼叫 PDO::beginTransaction。  
  
連接回到自動認可模式，如果此方法失敗。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
下列範例會使用名為 Test 的資料庫和名為 Table1 的資料表。 它會啟動交易並接著發出命令，以加入兩個資料列，然後再刪除一個資料列。 命令會傳送至資料庫，並以 `PDO::commit`明確地結束交易。  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
