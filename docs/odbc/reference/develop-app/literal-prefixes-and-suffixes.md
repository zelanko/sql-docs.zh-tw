---
title: 文字首碼與後綴 |微軟文件
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
ms.openlocfilehash: d52ca54c329353e3d9dc67ca35d89b2d28cedf74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287980"
---
# <a name="literal-prefixes-and-suffixes"></a>常值首碼及尾碼
在 SQL 語句中,*文本*是實際數據值的字元表示形式。 例如,在以下語句中,ABC、FFFF 和 10 是字面:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 某些資料類型的文字需要特殊的首碼和後綴。 在前面的範例中,字元文字 (ABC) 需要單個引號 (') 作為首碼和後綴,二進位元文本 (FFFF) 需要字元 0x 作為前置碼,整數文本 (10) 不需要前置碼或後綴。  
  
 對於除日期、時間和時間戳之外的所有數據類型,可互通的應用程式應使用**SQLGetTypeInfo**創建的結果集中返回的值LITERAL_PREFIX和LITERAL_SUFFIX列。 對於日期、時間、時間戳和日期時間間隔文本,可互操作的應用程式應使用上一節中討論的轉義序列。
