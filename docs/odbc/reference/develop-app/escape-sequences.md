---
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
ms.openlocfilehash: 5d9589230183b198cb7d59cf9739dab75625441e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298708"
---
# <a name="escape-sequences"></a>逸出序列
ODBC 定義包含日期、時間、時間戳和日期時間間隔文本、標量函數調用 **、LIKE**謂詞轉義字元、外部聯接和過程調用的標準語法的轉義序列。 可互通的應用程式應盡可能使用這些序列。  
  
 要確定驅動程式是否支援日期、時間、時間戳或日期時間間隔文字的轉義序列,應用程式呼叫**SQLGetTypeInfo**。 如果資料來源支援日期、時間、時間戳或日期時間間隔資料類型,則還必須支援相應的轉義序列。 要確定是否支援其他轉義序列,應用程式呼叫**SQLGetInfo**。  
  
 有關詳細資訊,請參閱[ODBC 中的轉義序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md),本節後面的後續操作。
