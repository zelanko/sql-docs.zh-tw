---
description: ODBC 轉譯程式子機碼
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46308518f1f806cea21bbb824312d5269f8b61e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499711"
---
# <a name="odbc-translators-subkey"></a>ODBC 轉譯程式子機碼
ODBC 轉譯子機碼底下的值會列出已安裝的轉換器。 這些值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**已安裝**|  
  
 *Translator-desc*名稱是由 translator developer 所定義。  
  
 例如，假設使用者已安裝 Microsoft®字碼頁翻譯工具和自訂 ASCII 至 EBCDIC 轉譯程式。 ODBC 轉譯子機碼底下的值可能如下所示：  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
