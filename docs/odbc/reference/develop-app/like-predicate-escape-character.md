---
title: 如述詞逸出字元 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30547551cc1793622eaa981c07bbc002d07a094d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312915"
---
# <a name="like-predicate-escape-character"></a>LIKE 述詞逸出字元
在 **像**述詞，百分比符號 （%）比對零或多個任意字元和底線 (_) 會比對任何單一字元。 比對實際的百分比符號或底線中**像**述詞，逸出字元必須在前面的百分比符號或底線。 定義逸出序列**像**述詞逸出字元是：  
  
 **{escape '** *escape-character* **'}**  
  
 何處*逸出字元*是資料來源所支援的任何字元。  
  
 如需類似的詳細資訊逸出序列，請參閱 <<c0> [ 逸出序列類似](../../../odbc/reference/appendixes/like-escape-sequence.md)附錄 c:SQL 文法。  
  
 例如，下列 SQL 陳述式建立相同的結果集，客戶的開頭是字元"%AAA"的名稱。 第一個陳述式會使用逸出序列的語法。 第二個陳述式為 Microsoft® Access 使用的原生的語法，而且不具互通性。 請注意，在每個字元的第二個百分比**像**述詞會比對零或多個任意字元的萬用字元。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 若要判斷是否**像是**述詞逸出字元支援的資料來源，應用程式會呼叫**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 選項。
