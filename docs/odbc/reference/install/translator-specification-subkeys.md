---
description: 轉譯程式規格子機碼
title: Translator 規格子機碼 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c02317c8abe12dbc693cdf7b715b6de84e5bc631
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461290"
---
# <a name="translator-specification-subkeys"></a>轉譯程式規格子機碼
ODBC translator 子機碼中列出的每個轉譯程式都有自己的子機碼。 這個子機碼與 ODBC 轉譯子機碼底下的對應值具有相同的名稱。 此子機碼底下的值會列出轉譯程式和轉譯程式安裝程式 Dll 的完整路徑，以及使用計數。 值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|Translator|REG_SZ|*translator-DLL-path*|  
|安裝程式|REG_SZ|*安裝程式-DLL-路徑*|  
|UsageCount|REG_DWORD|*計數*|  
  
 如需使用計數的詳細資訊，請參閱本節稍早的 [使用量計數](../../../odbc/reference/install/usage-counting.md) 。  
  
 應用程式不應該設定使用計數。 ODBC 將維持這個計數。  
  
 例如，假設 Microsoft 字碼頁翻譯工具有一個名為 Mscpxl32.dll 的轉譯 DLL、轉譯程式安裝程式的函式位於相同的 DLL 中，且翻譯工具已安裝三次。 Microsoft 字碼頁翻譯工具子機碼底下的值可能如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
