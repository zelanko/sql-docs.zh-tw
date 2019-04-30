---
title: ODBC 轉譯程式子機碼 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9e7109a6f1b88cf7639b2fc823ce0c5f14d05002
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280784"
---
# <a name="odbc-translators-subkey"></a>ODBC 轉譯程式子機碼
ODBC 轉譯程式子機碼下的值清單的已安裝的轉譯器。 下表顯示這些值的格式。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**安裝**|  
  
 *Translator desc*轉譯程式開發人員所定義名稱。  
  
 例如，假設使用者已安裝 Microsoft® 程式碼頁面轉譯器和自訂的 ASCII EBCDIC 轉譯程式。 ODBC 轉譯程式子機碼下的值可能如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
