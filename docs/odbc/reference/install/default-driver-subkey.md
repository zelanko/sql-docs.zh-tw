---
title: 預設驅動程式子機碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e82644d3bddab5d4f6fde6f7103bd9731872bab9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094193"
---
# <a name="default-driver-subkey"></a>預設驅動程式子機碼
預設子機碼包含描述的預設資料來源所使用的驅動程式的單一值。 下表顯示此值的格式。  
  
|名稱|資料類型|Data|  
|----------|---------------|----------|  
|**驅動程式**|REG_SZ|*default-driver-description*|  
  
 *預設驅動程式描述*名稱等同於底下說明驅動程式的 ODBC 驅動程式子機碼值的名稱。  
  
 比方說，如果預設的資料來源使用的 SQL Server 驅動程式，可能會將預設子機碼下的值：  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  預設的預設子機碼中包含的驅動程式可以參考的預設使用者 DSN 或預設系統 DSN。 如果預設的使用者 DSN 與預設系統尚未建立 DSN，預設的驅動程式取決於最後，建立 DSN 因此，可能不需要先建立資料來源名稱的有效項目。
