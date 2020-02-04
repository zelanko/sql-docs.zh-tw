---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f94c20c8aa6cf603c6588586e072813682b2ce68
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67992696"
---
# <a name="sqlsrv_get_config"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回指定的組態設定目前的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>參數  
*$setting*：對其傳回值的組態設定。 如需可設定的設定清單，請參閱＜ [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)＞。  
  
## <a name="return-value"></a>傳回值  
*$setting* 參數所指定的設定值。 如果指定了無效的設定，則會傳回 **false** 並將一個錯誤加入至錯誤集合。  
  
## <a name="remarks"></a>備註  
如果 **false** config **sqlsrv_get_config**，您必須呼叫 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) 以判斷是否發生錯誤，或者 **false** 是否為 *$setting* 參數所指定的設定值。  
  
## <a name="see-also"></a>另請參閱  
[SQLSRV 驅動程式 API 參考](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
