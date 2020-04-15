---
title: ODBC 翻譯器子鍵 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296218"
---
# <a name="odbc-translators-subkey"></a>ODBC 轉譯程式子機碼
ODBC 翻譯人員子鍵下的值列出了已安裝的譯員。 這些值的格式顯示在下表中。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*譯者-德茨*|REG_SZ|**安裝**|  
  
 *翻譯器-desc*名稱由轉換器開發人員定義。  
  
 例如,假設使用者已安裝 Microsoft ®代碼頁轉換器和自訂 ASCII 到 EBCDIC 轉換器。 ODBC 翻譯人員子鍵下的值可能如下所示:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
