---
title: "述詞的逸出字元像 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 132359972cebd3dded36fb911a2ee8e561e5ca64
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="like-predicate-escape-character"></a>像述詞的逸出字元
在**像**述詞，百分比符號 （%） 比對零個或多個任意字元和底線 (_) 符合任何一個字元。 符合實際的百分比符號或底線中**像**述詞，逸出字元必須放在之前的百分比符號或底線。 定義的逸出序列**像**述詞的逸出字元是：  
  
 **{逸出 '** *逸出字元* **'}**  
  
 其中*逸出字元*是任何資料來源所支援的字元。  
  
 如需 LIKE 逸出序列，請參閱 <<c0> [ 逸出序列類似](../../../odbc/reference/appendixes/like-escape-sequence.md)附錄 c: SQL 文法中。  
  
 例如，下列 SQL 陳述式建立相同的結果集之客戶的字母"%AAA"為開頭的名稱。 第一個陳述式會使用逸出序列語法。 第二個陳述式為 Microsoft® Access 使用的原生的語法，且不互通。 請注意，在每個字元的第二個百分比**像**述詞是比對零或多個任意字元的萬用字元。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 若要判斷是否**像**述詞的逸出字元支援的資料來源，應用程式呼叫**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 選項。

