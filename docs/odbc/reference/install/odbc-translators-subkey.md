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
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093946"
---
# <a name="odbc-translators-subkey"></a>ODBC 轉譯程式子機碼
ODBC 轉譯程式子機碼下的值清單的已安裝的轉譯器。 下表顯示這些值的格式。  
  
|名稱|資料類型|Data|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**安裝**|  
  
 *Translator desc*轉譯程式開發人員所定義名稱。  
  
 例如，假設使用者已安裝 Microsoft® 程式碼頁面轉譯器和自訂的 ASCII EBCDIC 轉譯程式。 ODBC 轉譯程式子機碼下的值可能如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
