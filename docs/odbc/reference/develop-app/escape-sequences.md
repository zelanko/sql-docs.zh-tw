---
description: 逸出序列
title: 逸出序列 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15c06fc08d78422502b8aea87c40ee2821a9620f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429300"
---
# <a name="escape-sequences"></a>逸出序列
ODBC 會定義包含日期、時間、時間戳記和日期時間間隔常值、純量函式呼叫（ **例如** 述詞 escape 字元、外部聯結和程序呼叫）之標準文法的 escape 序列。 可互通的應用程式應該盡可能使用這些序列。  
  
 若要判斷驅動程式是否支援日期、時間、時間戳記或日期時間間隔常值的 escape 序列，應用程式會呼叫 **SQLGetTypeInfo**。 如果資料來源支援 date、time、timestamp 或 datetime interval 資料類型，則它也必須支援對應的 escape 序列。 為了判斷是否支援其他的 escape 序列，應用程式會呼叫 **SQLGetInfo**。  
  
 如需詳細資訊，請參閱本節稍後的 [ODBC 中的 Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
