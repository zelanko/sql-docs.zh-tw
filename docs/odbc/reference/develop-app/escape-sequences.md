---
title: 逸出序列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2e9dc60d4cb598c777527aa6825ef2ee3a35b2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="escape-sequences"></a>逸出序列
ODBC 定義逸出序列，其中包含日期、 時間、 時間戳記和日期時間間隔常值的純量函式呼叫，標準文法**像**述詞的逸出字元、 外部聯結，以及程序呼叫。 互通的應用程式應該使用盡可能這些順序。  
  
 若要判斷驅動程式是否支援日期、 時間、 時間戳記，或日期時間間隔的常值的逸出序列，應用程式呼叫**SQLGetTypeInfo**。 如果資料來源支援日期、 時間、 時間戳記或日期時間間隔資料類型，它也必須支援對應的逸出序列。 若要判斷是否支援的逸出序列，應用程式呼叫**SQLGetInfo**。  
  
 如需詳細資訊，請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)稍後這一節。
