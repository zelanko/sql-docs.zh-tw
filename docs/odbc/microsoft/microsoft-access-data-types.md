---
title: Microsoft Access 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b99fd70e0119aa01d384066aaa2f3b91eed152b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026897"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 資料類型
下表顯示 Microsoft Access 資料類型、 資料類型用來建立資料表，以及 ODBC SQL 資料類型。  
  
|Microsoft Access 資料類型|資料類型 (CREATETABLE)|ODBC SQL 資料類型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY[1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|計數器|計數器|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|日期/時間|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|長的二進位|LONGBINARY|SQL_LONGVARBINARY|  
|長文字|長文字|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|附註|長文字|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|數字 (欄位大小 = 單一)|單一|SQL_REAL|  
|數字 (欄位大小 = 雙精度浮點數)|DOUBLE|SQL_DOUBLE|  
|數字 (欄位大小 = BYTE)|不帶正負號的位元組|SQL_TINYINT|  
|NUMBER (FieldSize= INTEGER)|簡短|SQL_SMALLINT|  
|數字 (欄位大小 = 長整數)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 存取 4.0 應用程式。 最大長度 4000 個位元組。 LONGBINARY 類似的行為。  
  
 [2] ANSI 應用程式。  
  
 [3] Unicode 和存取 4.0 應用程式。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC 資料類型。 如果一個以上的 Microsoft Access 類型會對應至相同的 ODBC SQL 資料類型，它不會傳回所有的 Microsoft Access 資料型別。 附錄 D 中的所有轉換*ODBC 程式設計人員參考*支援上表中列出的 SQL 資料類型。  
  
 下表顯示在 Microsoft Access 資料類型上的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|二進位、 VARBINARY 和 VARCHAR|建立 BINARY、 VARBINARY 或 VARCHAR 資料行的零或未指定的長度實際上會傳回 510 位元組的資料行。|  
|BYTE|即使 Microsoft 存取號碼欄位與欄位大小等於位元組不帶正負號，負數可插入的欄位時使用 Microsoft Access 驅動程式。|  
|CHAR、 LONGVARCHAR、 和 VARCHAR|字元字串常值可以包含任何 ANSI 字元 （1-255 十進位）。 您可以使用兩個連續單引號 （'） 來表示一個單引號 （'）。<br /><br /> 將字元資料使用字元資料類型資料行中的任何特殊字元時應程序。|  
|DATE|日期值必須根據 ODBC 標準的日期格式分隔或以日期時間的分隔符號 （"#"） 分隔。 否則，Microsoft Access 會將值視為算術運算式，而且將不會引發警告或錯誤。<br /><br /> 例如，"1996 年 3 月 5 日 」 都必須表示成日期 {d ' 1996年-03-05'} 或 #03/05/1996年 #;否則，只有 03/05/1993年提交時，Microsoft Access 會評估這為 3 除以 5 除以 1996年。 這個值會無條件進位到整數 0，，和零時差會對應至 1899年-12-31，因為這是使用的日期。<br /><br /> 直立線符號字元 (&#124;) 不能在日期值，即使在上一步括引號括住。|  
|GUID|限制為 Microsoft Access 4.0 資料類型。|  
|NUMERIC|限制為 Microsoft Access 4.0 資料類型。|  
  
 資料型別上的更多限制可在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。
