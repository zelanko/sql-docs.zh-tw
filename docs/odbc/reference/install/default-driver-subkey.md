---
title: "預設驅動程式的子機碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5c269705f5e4c0c855b5b7f929b1a76ee9523bd7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="default-driver-subkey"></a>預設驅動程式的子機碼
預設子機碼包含描述的預設資料來源所使用的驅動程式的單一值。 下表顯示此值的格式。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|**驅動程式**|REG_SZ|*預設驅動程式說明*|  
  
 *預設驅動程式描述*名稱是描述驅動程式的 ODBC 驅動程式子機碼下值的名稱相同。  
  
 例如，如果預設的資料來源會使用 SQL Server 驅動程式，可能是預設子機碼下的值：  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  預設子機碼中包含的預設驅動程式可以參考的預設使用者 DSN 或預設的系統 DSN。 如果預設使用者 DSN 與預設系統 DSN 尚未建立，預設的驅動程式取決於 DSN 建立最後，因此它可能不會先建立資料來源名稱的有效項目。

