---
title: 常值前置詞和尾碼 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d1d836c086747cba5b42b0db5a1919575afcfaa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="literal-prefixes-and-suffixes"></a>常值前置詞和尾碼
SQL 陳述式中*常值*是實際資料值的字元表示法。 例如，下列陳述式中，ABC、 FFFF 和 10 是常值：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 某些資料類型的常值需要特殊的前置詞和後置字元。 在上述範例中，字元常值 (ABC) 需要單引號 （'） 做為前置詞和後置詞，而二進位常值 (FFFF) 需要的字元 0x 前置詞，以及整數常值 (10) 不需要前置詞或後置詞。  
  
 日期、 時間和時間戳記以外的所有資料型別，可互通的應用程式應該都使用 LITERAL_PREFIX 和 LITERAL_SUFFIX 資料行中所建立的結果集中傳回的值**SQLGetTypeInfo**。 針對日期、 時間、 時間戳記和日期時間間隔的常值，可互通的應用程式應該使用上一節中討論的逸出序列。
