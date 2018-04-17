---
title: Microsoft Access 資料型別 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8faac619846998c1be7bc0577761b94bf6dc27ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 資料類型
下表顯示 Microsoft Access 資料型別、 用來建立資料表、 資料型別和 ODBC SQL 資料類型。  
  
|Microsoft Access 資料類型|資料型別 (CREATETABLE)|ODBC SQL 資料類型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|計數器|計數器|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|日期/時間|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|長的二進位|LONGBINARY|SQL_LONGVARBINARY|  
|長文字|長文字|[2] 的 SQL_LONGVARCHAR SQL_WLONGVARCHAR [3]|  
|附註|長文字|[2] 的 SQL_LONGVARCHAR SQL_WLONGVARCHAR [3]|  
|數字 (大小 = 單一)|單一|SQL_REAL|  
|數字 (大小 = 雙)|DOUBLE|SQL_DOUBLE|  
|數字 (大小 = 位元組)|不帶正負號的位元組|SQL_TINYINT|  
|數字 (大小 = 整數)|短|SQL_SMALLINT|  
|數字 (大小 = 長整數)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|[1] SQL_VARCHAR SQL_WVARCHAR [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 存取只有 4.0 應用程式。 最大長度 4000 個位元組。 LONGBINARY 類似的行為。  
  
 [2] ANSI 應用程式。  
  
 [Unicode 3] 和存取 4.0 應用程式。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC 資料類型。 如果一個以上的 Microsoft Access 類型會對應至相同的 ODBC SQL 資料類型，它不會傳回所有的 Microsoft Access 資料型別。 所有的轉換中的 < 附錄 D *ODBC 程式設計人員參考*支援上表中列出的 SQL 資料類型。  
  
 下表顯示 Microsoft Access 資料類型的限制。  
  
|資料類型|Description|  
|---------------|-----------------|  
|二進位、 VARBINARY 和 VARCHAR|建立二進位、 VARBINARY 或 VARCHAR 資料行的零或未指定的長度實際上會傳回 510 位元組的資料行。|  
|BYTE|即使 Microsoft 存取號碼欄位與欄位大小等於位元組不帶正負號，負數可以插入到欄位，使用 Microsoft Access 驅動程式時。|  
|CHAR、 LONGVARCHAR 和 VARCHAR|字元字串常值可以包含任何的 ANSI 字元 （1-255 個十進位）。 您可以使用兩個連續單引號 （'） 來表示一個單引號 （'）。<br /><br /> 程序應該用來傳遞字元資料時使用字元資料類型資料行中的任何特殊字元。|  
|DATE|日期值必須根據 ODBC 標準日期格式分隔或 datetime 分隔符號 （"#"） 分隔。 否則，Microsoft Access 會將值視為算術運算式，而且將不會引發警告或錯誤。<br /><br /> 例如，"1996 年 3 月 5 日 」 必須表示成日期 {d ' 1996年-03-05'} 或 1996 #03/05 / #;否則，如果只提交 03/05/1993年，Microsoft Access 會評估這 3 除以 5 除以 1996年為。 這個值會無條件進位到 0 的整數，零一天對應至 1899年-12-31，因為這是所使用的日期。<br /><br /> 縱線字元 (&#124;) 不能在日期值，即使在回括引號。|  
|GUID|限制為 Microsoft Access 4.0 資料類型。|  
|NUMERIC|限制為 Microsoft Access 4.0 資料類型。|  
  
 資料類型的多個限制可以在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。
