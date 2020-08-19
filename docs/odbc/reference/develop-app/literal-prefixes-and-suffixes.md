---
description: 常值首碼及尾碼
title: 常值首碼和尾碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f658c401bfc31e69a6e5e2fc5110bc9a809f345
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424610"
---
# <a name="literal-prefixes-and-suffixes"></a>常值首碼及尾碼
在 SQL 語句中， *常* 值是實際資料值的字元標記法。 例如，在下列語句中，ABC、FFFF 和10是常值：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 某些資料類型的常值需要特殊的首碼和尾碼。 在上述範例中，字元常值 (ABC) 需要單引號 ( ' ) 做為前置詞和後置詞，二進位常值 (FFFF) 要求字元0x 做為前置詞，而整數常值 (10) 不需要前置詞或尾碼。  
  
 對於日期、時間和時間戳記以外的所有資料類型，可互通的應用程式應該使用 LITERAL_PREFIX 中傳回的值，以及 **SQLGetTypeInfo**所建立之結果集中的 LITERAL_SUFFIX 資料行。 針對日期、時間、時間戳記和日期時間間隔常值，可互通的應用程式應使用上一節所討論的 escape 序列。
