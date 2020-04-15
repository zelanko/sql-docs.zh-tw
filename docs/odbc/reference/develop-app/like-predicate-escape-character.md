---
title: 喜歡謂詞轉義字元 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e4f04b12911145eede3354532736cb92f1ae413
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306149"
---
# <a name="like-predicate-escape-character"></a>LIKE 述詞逸出字元
在**LIKE**謂詞中,百分比符號 (%)匹配任何字元的零個或多個,下劃線 (*) 匹配任何一個字元。 要匹配**LIKE**謂詞中的實際百分比符號或下劃線,轉義字元必須位於百分比符號或下劃線之前。 定義**LIKE**謂詞轉義字元的轉義序列是:  
  
 **[逃生字元***escape-character***]**  
  
 其中*轉義字元*是數據源支援的任何字元。  
  
 有關 LIKE 轉義序列的詳細資訊,請參閱附錄 C 中的[「LIKE 轉義序列](../../../odbc/reference/appendixes/like-escape-sequence.md)」:SQL 語法。  
  
 例如,以下 SQL 語句建立以字元「%AAA」開頭的客戶名稱的相同結果集。 第一個語句使用轉義序列語法。 第二個語句使用 Microsoft ®訪問的原生語法,並且不可互通。 請注意,每個**LIKE**謂詞中的第二個百分比字元是匹配任何字元的零個或多個的通配符。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 要確定資料來源是否支援**LIKE**謂詞轉義字元,應用程式使用SQL_LIKE_ESCAPE_CLAUSE選項呼叫**SQLGetInfo。**
