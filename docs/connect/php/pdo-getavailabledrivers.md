---
title: "Pdo:: getavailabledrivers |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f9df73c378da9caf8165f4703c954542df97dc2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回您的 PHP 安裝中的 PDO 驅動程式陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>傳回值  
包含 PDO 驅動程式清單的陣列。  
  
## <a name="remarks"></a>備註  
PDO 驅動程式的名稱用於 PDO::__construct，以建立 PDO 執行個體。  
  
PDO::getAvailableDrivers 不需要由 PHP 驅動程式實作。 如需有關此方法的詳細資訊，請參閱 PHP 文件。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

