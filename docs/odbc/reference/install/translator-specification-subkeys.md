---
title: "轉譯器規格子機碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62bfe54f5bd5117fee5d9ba063f1882be47ccbc4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="translator-specification-subkeys"></a>轉譯器規格子機碼
ODBC 轉譯子機碼中所列每個轉譯器都有自己的子機碼。 這個子機碼具有 ODBC 轉譯子機碼下的對應值相同的名稱。 這個子機碼下的值清單之轉譯器轉譯程式安裝 Dll 並使用計數的完整路徑。 值的格式是下表所示。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|轉譯程式|REG_SZ|*轉譯程式 DLL 路徑*|  
|安裝程式|REG_SZ|*安裝程式 DLL 路徑*|  
|UsageCount|REG_DWORD|*計數*|  
  
 如需使用方式計數資訊，請參閱[使用量計算](../../../odbc/reference/install/usage-counting.md)稍早在這一節。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護這個計數。  
  
 例如，假設 Microsoft 程式碼頁面轉譯器具有名為 Mscpxl32.dll 轉譯器的安裝程式函式位於相同的 DLL，DLL 的翻譯和轉譯程式確認已安裝三次。 Microsoft 的程式碼頁面轉譯器的子機碼下的值可能如下所示：  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```

