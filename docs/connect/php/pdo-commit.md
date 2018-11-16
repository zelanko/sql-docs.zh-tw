---
title: 'Pdo:: commit |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f30119d7fb8d2e1f23b719273738cc52cf3b7d00
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606328"
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

將在呼叫 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 之後發出的命令傳送至資料庫，並且讓連接回到自動認可模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>傳回值  
如果方法呼叫成功，會傳回 true，否則傳回 false。  
  
## <a name="remarks"></a>Remarks  
PDO::commit 不受 PDO::ATTR_AUTOCOMMIT 的值影響 (且不會影響該值)。  
  
如需使用 PDO::commit 的範例，請參閱 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
