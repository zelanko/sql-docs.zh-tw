---
title: 翻譯工具規格子機碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec94f3e02b720617e8f7369b12a916c2bbbe7b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093802"
---
# <a name="translator-specification-subkeys"></a>轉譯程式規格子機碼
ODBC 轉譯子機碼中所列的每個翻譯工具都有自己的子機碼。 這個子機碼的名稱與 ODBC 轉譯子機碼底下對應的值相同。 此子機碼底下的值會列出 translator 和 translator 安裝程式 Dll 的完整路徑，以及使用計數。 值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|翻譯|REG_SZ|*translator-DLL-路徑*|  
|安裝程式|REG_SZ|*安裝程式-DLL-路徑*|  
|UsageCount|REG_DWORD|*計數*|  
  
 如需使用計數的詳細資訊，請參閱本節稍早的[使用量計數](../../../odbc/reference/install/usage-counting.md)。  
  
 應用程式不應該設定使用計數。 ODBC 會維護此計數。  
  
 例如，假設 Microsoft 字碼頁翻譯工具具有名為 Mscpxl32 的轉譯 DLL，則 translator 安裝程式會在相同的 DLL 中，而且翻譯工具已安裝三次。 Microsoft 字碼頁 Translator 子機碼底下的值可能如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
