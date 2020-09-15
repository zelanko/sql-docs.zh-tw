---
description: sqlsrv_configure
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c99aff2e8453a2c2d16db34894935d5b1f7e5ff5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413864"
---
# <a name="sqlsrv_configure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

變更錯誤處理和記錄選項的設定。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>參數  
*$setting*：要設定的設定名稱。 請參閱下表中的設定清單。  
  
*$value*：要對 *$setting* 參數中指定的設定套用的值。 此參數的可能值取決所指定的設定。 下表列出可能的組合。  
  
|設定|$value 參數的可能值 (括號中的整數對等項目)|預設值|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|不超過 PHP 記憶體限制的非負數。<br /><br />不允許使用零和負數。|10240 KB|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL (-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR (1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE (4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING (2)|SQLSRV_LOG_SEVERITY_ERROR (1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL (-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN (2)<br /><br />SQLSRV_LOG_SYSTEM_INIT (1)<br /><br />SQLSRV_LOG_SYSTEM_OFF (0)<br /><br />SQLSRV_LOG_SYSTEM_STMT (4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL (8)|SQLSRV_LOG_SYSTEM_OFF (0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true** (1) 或 **false** (0)|**true** (1)|  
  
## <a name="return-value"></a>傳回值  
如果以不受支援的設定或值呼叫 **sqlsrv_configure** ，函數會傳回 **false**。 否則，函數會傳回 **true**。  
  
## <a name="remarks"></a>備註  
(1) 如需用戶端查詢的詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)。  
  
(2) 如需記錄活動的詳細資訊，請參閱[記錄活動](../../connect/php/logging-activity.md)。  
  
(3) 如需關於設定錯誤和警告處理的詳細資訊，請參閱[如何：使用 SQLSRV 驅動程式設定錯誤和警告處理](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)

[Microsoft Drivers for PHP for SQL Server 的程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
