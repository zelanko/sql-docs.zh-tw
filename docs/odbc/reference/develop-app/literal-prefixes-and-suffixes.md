---
title: 常值前置詞和後置詞 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4eabc3e0c354e02ad8df790d896dc43ae49c9bd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680856"
---
# <a name="literal-prefixes-and-suffixes"></a>常值首碼及尾碼
在 SQL 陳述式中，*常值*是實際資料值的字元表示法。 比方說，在下列陳述式，ABC、 FFFF 和 10 是常值：  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 某些資料類型的常值需要特殊的前置詞和後置詞。 在上述範例中，字元常值 (ABC) 需要單引號 （'） 做為前置詞和尾碼，二進位常值 (FFFF) 需要的 0x 前置詞，以及整數常值 (10) 不需要前置詞或後置字元的字元。  
  
 針對日期、 時間和時間戳記以外的所有資料類型，可互通的應用程式應該使用 LITERAL_PREFIX 和 LITERAL_SUFFIX 資料行中所建立的結果集中傳回的值**SQLGetTypeInfo**。 針對日期、 時間、 時間戳記和日期時間間隔常值，可互通的應用程式應該使用上一節所述的逸出序列。
