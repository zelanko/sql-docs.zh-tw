---
title: ODBC 轉譯子機碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093946"
---
# <a name="odbc-translators-subkey"></a>ODBC 轉譯程式子機碼
ODBC 轉譯子機碼底下的值會列出已安裝的轉譯者。 下表顯示這些值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**客戶**|  
  
 Translator *-desc*名稱是由 translator developer 所定義。  
  
 例如，假設使用者已安裝 Microsoft®字碼頁翻譯工具，以及自訂的 ASCII 至 EBCDIC 轉譯程式。 ODBC 轉譯子機碼底下的值可能如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
