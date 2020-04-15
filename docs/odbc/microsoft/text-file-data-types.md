---
title: 文字檔案資料型態 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7864dc81eaa3dd37f3d0053b2329c8842e445c8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302656"
---
# <a name="text-file-data-types"></a>文字檔資料類型
下表顯示了文本資料類型如何映射到 ODBC SQL 資料類型。 請注意,ODBC 文本驅動程式並非支援所有 ODBC SQL 資料類型。  
  
|文字資料類型|ODBC 資料類型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|朗查爾|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC 資料類型。 對於上表中列出的 SQL 資料類型,支援*ODBC 程式師參考*附錄 D 中的所有轉換。  
  
 下表顯示了對文本數據類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|CHAR|創建零或未指定長度的 CHAR 列實際上返回 255 位列。<br /><br /> 在分隔檔中,CHAR 列在開頭和結尾可能具有雙引號分隔符,也可能沒有雙引號分隔符;在固定長度檔中,雙引號不用作分隔符。|  
|DATETIME|MM-DD-YY(例如,01-17-92)<br /><br /> MMM-DD-YY(例如,1月17-92日)<br /><br /> DD-MMM-YY(例如,1月17日-92)<br /><br /> YYYY-MM-DD(例如,1992-01-17)<br /><br /> YYYY-MMM-DD(例如,1992年-1月-17日)<br /><br /> 不允許在表中混合日期分隔符。<br /><br /> "文字 ISAM"以美國或歐洲格式設置 DATETIME 欄位,具體取決於 Windows 控制面板中的"國際"設置。|  
|FLOAT|最大寬度包括符號和小數點。 在 Schema.ini 中,寬度表示如下:<br /><br /> 14.083 是 FLOAT 寬度 6<br /><br /> -14.083 是 FLOAT 寬度 7<br /><br /> +14.083 是 FLOAT 寬度 7<br /><br /> 14083. 是 FLOAT 寬度 6<br /><br /> ODBC 始終為 FLOAT 列返回 8。<br /><br /> FLOAT 列也可以使用科學記數法,例如:<br /><br /> -3.04E+2 是浮動寬度 8<br /><br /> 25E4 是浮動寬度 4<br /><br /> **注意**十進制和科學記數法不能混合在列中。<br /><br /> NULL 值由固定長度檔中的空白填充字串表示,並在分隔檔中省略。<br /><br /> 浮動數據可以使用前導空格填充。|  
|INTEGER|INTEGER 列的有效值為 32767 到 -32766。<br /><br /> 在 Schema.ini 中,寬度表示如下:<br /><br /> 14083 是 INTEGER 寬度 5<br /><br /> 0 是整合寬度 1<br /><br /> ODBC 始終為 INTEGER 列返回 4。<br /><br /> 最大寬度包括一個符號。 INTEGER 列的最大寬度為 11,儘管由於固定格式表中允許的空白,寬度可能更大。|  
|朗查爾|固定長度或分隔表中 LONGCHAR 列寬度的理論限製為 65500K。 文本 ISAM 更有可能提供高達 32K 的可靠支援。|  
  
 數據類型的更多限制可以在[數據類型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
