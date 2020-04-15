---
title: 預設驅動程式子鍵 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb134d670964e352d94c13474d8a72fa4bd494ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301051"
---
# <a name="default-driver-subkey"></a>預設驅動程式子機碼
預設子鍵包含描述預設資料來源使用的驅動程式的單個值。 此值的格式顯示在下表中。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|**司機**|REG_SZ|*預設驅動程式描述*|  
  
 *預設驅動程式描述*名稱與描述驅動程式的 ODBC 驅動程式子鍵下的值名稱相同。  
  
 例如,如果預設資料來源使用 SQL Server 驅動程式,則預設子鍵下的值可能是:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  默認子鍵中包含的預設驅動程式可以引用預設使用者 DSN 或預設系統 DSN。 如果已創建預設使用者 DSN 和預設系統 DSN,則預設驅動程式由上次創建的 DSN 確定,因此可能不是首先創建的 DSN 的有效條目。
