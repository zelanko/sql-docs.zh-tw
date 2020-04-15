---
title: 轉換器規格子鍵 |微軟文件
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
ms.openlocfilehash: ad21943c5313edcb09aba88d45ea21132aa9757f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296038"
---
# <a name="translator-specification-subkeys"></a>轉譯程式規格子機碼
ODBC 翻譯人員子鍵中列出的每個轉換器都有其自己的子密鑰。 此子鍵的名稱與 ODBC 翻譯器子鍵下的相應值相同。 此子鍵下的值列出了轉換器和轉換器設置 DLL 的完整路徑和使用計數。 值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|轉譯程式|REG_SZ|*轉換器-DLL 路徑*|  
|安裝程式|REG_SZ|*設定-DLL路徑*|  
|使用方式計數|REG_DWORD|*count*|  
  
 有關使用方式計數的資訊,請參閱本節前面[先查看使用方式計數](../../../odbc/reference/install/usage-counting.md)。  
  
 應用程式不應設置使用計數。 ODBC 將保留此計數。  
  
 例如,假設 Microsoft 代碼頁轉換器具有名為 Mscpxl32.dll 的翻譯 DLL,其中譯員的設置功能位於同一 DLL 中,並且譯員已安裝三次。 Microsoft 代碼頁翻譯子鍵下的值可能如下所示:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
