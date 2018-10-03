---
title: 'Pdo:: rollback |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f5f33f7d027a858bdd57aa69c65107ed15856e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609242"
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

捨棄在呼叫 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 之後所發出的資料庫命令，並且讓連接返回自動認可模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>傳回值  
如果方法呼叫成功，會傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>Remarks  
PDO::rollback 不受 PDO::ATTR_AUTOCOMMIT 的值影響 (且不會影響該值)。  
  
如需使用 PDO::rollback 的範例，請參閱 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
