---
title: 文字檔資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 829f924d8d4893d45a48c193cd27fdd7ac261e3d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939717"
---
# <a name="text-file-data-types"></a>文字檔資料類型
下表顯示文字資料類型對應至 ODBC SQL 資料類型的方式。 請注意，ODBC 文字驅動程式並不支援所有的 ODBC SQL 資料類型。  
  
|Text 資料類型|ODBC 資料類型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**會傳回 ODBC 資料類型。 針對上表所列的 SQL 資料類型，支援 ODBC 程式設計*人員參考*附錄 D 中的所有轉換。  
  
 下表顯示文字資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|CHAR|建立零或未指定長度的 CHAR 資料行，實際上會傳回255位資料行。<br /><br /> 在分隔的檔案中，CHAR 資料行的開頭和結尾不一定會有雙引號分隔符號;在固定長度的檔案中，不會使用雙引號做為分隔符號。|  
|DATETIME|MM-DD-YY （例如，01-17-92）<br /><br /> MMM-DD-YY （例如，Jan-17-92）<br /><br /> DD-MMM-YY （例如，17-Jan-92）<br /><br /> YYYY-MM-DD （例如，1992-01-17）<br /><br /> YYYY MMM-DD （例如，1992-Jan-17）<br /><br /> 資料表中不允許有混合的日期分隔符號。<br /><br /> 文字 [ISAM] 會根據 Windows [控制台] 中的 [國際] 設定，格式化 [美國] 或 [歐洲] 格式的日期時間欄位。|  
|FLOAT|最大寬度包含正負號和小數點。 在 schema.ini 中，寬度的表示方式如下：<br /><br /> 14.083 為 FLOAT 寬度6<br /><br /> -14.083 為 FLOAT 寬度7<br /><br /> + 14.083 是浮動寬度7<br /><br /> 14083。是 FLOAT 寬度6<br /><br /> ODBC 的 FLOAT 資料行一律會傳回8。<br /><br /> FLOAT 資料行也可以是科學記號標記法，例如：<br /><br /> -3.04 e + 2 是 Float 寬度8<br /><br /> 25E4 是 Float 寬度4<br /><br /> **注意**十進位和科學標記法不能在資料行中混用。<br /><br /> Null 值是以固定長度檔案中空白填補的字串表示，並在分隔的檔案中省略。<br /><br /> 浮動資料可以填補開頭的空白。|  
|INTEGER|整數資料行的有效值為32767到-32766。<br /><br /> 在 schema.ini 中，寬度的表示方式如下：<br /><br /> 14083是整數寬度5<br /><br /> 0是整數寬度1<br /><br /> 對於整數資料行，ODBC 一律會傳回4。<br /><br /> 寬度上限包含正負號。 整數資料行的最大寬度為11，雖然寬度可能會因為固定格式資料表中允許的空白而增加。|  
|LONGCHAR|在固定長度或分隔的資料表中，LONGCHAR 資料行寬度的理論限制為65500K。 Text ISAM 較可能提供可靠的支援（最多大約32K）。|  
  
 您可以在[資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
