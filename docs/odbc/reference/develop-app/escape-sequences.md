---
title: Escape 序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001378"
---
# <a name="escape-sequences"></a>逸出序列
ODBC 會定義包含日期、時間、時間戳記和日期時間間隔常值之標準文法的逸出序列、純量函式呼叫，**例如**述詞逸出字元、外部聯結和程序呼叫。 互通的應用程式應該盡可能使用這些序列。  
  
 若要判斷驅動程式是否支援日期、時間、時間戳記或日期時間間隔常值的轉義順序，應用程式會呼叫**SQLGetTypeInfo**。 如果資料來源支援日期、時間、時間戳記或日期時間間隔資料類型，它也必須支援對應的逸出序列。 為了判斷是否支援其他的逸出序列，應用程式會呼叫**SQLGetInfo**。  
  
 如需詳細資訊，請參閱本節稍後的[ODBC 中的 Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
