---
title: 轉譯程式規格子機碼 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a3c5ad31437cf2639d6b8478d173c7522fa3e9fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63272936"
---
# <a name="translator-specification-subkeys"></a>轉譯程式規格子機碼
ODBC 轉譯程式子機碼中所列每 translator 都有自己的子機碼。 這個子機碼具有相同名稱做為 ODBC 轉譯程式子機碼下對應的值。 這個子機碼底下的值清單轉譯器轉譯程式安裝程式 Dll 並使用計數的完整的路徑。 值的格式是下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|轉譯程式|REG_SZ|*translator-DLL-path*|  
|安裝程式|REG_SZ|*setup-DLL-path*|  
|UsageCount|REG_DWORD|*計數*|  
  
 如需使用方式計數資訊，請參閱[使用量計算](../../../odbc/reference/install/usage-counting.md)稍早在這一節。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護此計數。  
  
 例如，假設 Microsoft 程式碼頁面轉譯器具有名為 Mscpxl32.dll，轉譯器設定函式位於相同的 DLL，DLL 的翻譯，而且此轉譯程式，已安裝三次。 Microsoft 的程式碼頁面轉譯程式子機碼下的值可能如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
