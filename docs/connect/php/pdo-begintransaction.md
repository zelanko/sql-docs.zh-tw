---
title: "Pdo:: begintransaction |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c65de9c08dd4d92480c855378516850814ecd6b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
以 PDO::beginTransaction 開始的交易，會在呼叫 [PDO::commit](../../connect/php/pdo-commit.md) 或 [PDO::rollback](../../connect/php/pdo-rollback.md) 時結束。  
  
PDO::beginTransaction 不受 PDO::ATTR_AUTOCOMMIT 的值影響 (且不會影響該值)。  
  
在使用 PDO::rollback 或 PDO::commit 結束先前的 PDO::beginTransaction 之前，您無法呼叫 PDO::beginTransaction。  
  
如果此方法失敗，連接將會回到自動認可模式。  
  
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
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

