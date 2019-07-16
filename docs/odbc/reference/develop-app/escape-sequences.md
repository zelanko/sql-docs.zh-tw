---
title: 逸出序列 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001378"
---
# <a name="escape-sequences"></a>逸出序列
ODBC 定義包含日期、 時間、 時間戳記和日期時間間隔常值的純量函式呼叫，標準文法的逸出序列**像**述詞逸出字元、 外部聯結和程序呼叫。 互通的應用程式應該使用這些盡可能的序列。  
  
 若要判斷是否驅動程式支援的逸出序列的日期、 時間、 時間戳記，或日期時間間隔常值，應用程式會呼叫**SQLGetTypeInfo**。 如果資料來源支援日期、 時間、 時間戳記或日期時間間隔資料類型，它也必須支援對應的逸出序列。 若要判斷是否支援的逸出序列，應用程式會呼叫**SQLGetInfo**。  
  
 如需詳細資訊，請參閱 < [ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)稍後這一節。
