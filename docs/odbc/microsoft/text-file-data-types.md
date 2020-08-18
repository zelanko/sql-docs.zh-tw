---
description: 文字檔資料類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d14d98f7aa25c42ec6d121aa0819a1f3dcce5db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449100"
---
# <a name="text-file-data-types"></a>文字檔資料類型
下表解說文字資料類型如何對應至 ODBC SQL 資料類型。 請注意，ODBC 文字驅動程式並不支援所有的 ODBC SQL 資料類型。  
  
|Text 資料類型|ODBC 資料類型|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 會傳回 ODBC 資料類型。 上表所列的 SQL 資料類型支援 ODBC 程式設計 *人員參考* 附錄 D 中的所有轉換。  
  
 下表顯示文字資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|CHAR|建立零或未指定長度的 CHAR 資料行實際上會傳回255位資料行。<br /><br /> 在分隔檔案中，CHAR 資料行的開頭和結尾可能會有雙引號分隔符號;在固定長度的檔案中，不會使用雙引號做為分隔符號。|  
|DATETIME|MM DD-YY (例如 01-17-92) <br /><br /> MMM DD-YY (例如 Jan-17-92) <br /><br /> DD-YY (例如 17-Jan-92) <br /><br /> YYYY-MM-DD (例如 1992-01-17) <br /><br /> YYYY MMM (例如 1992-Jan-17) <br /><br /> 資料表中不允許使用混合的日期分隔符號。<br /><br /> 文字 ISAM 會根據 Windows 主控台中的國際設定，根據美國或歐洲格式來格式化 DATETIME 欄位。|  
|FLOAT|最大寬度包含正負號和小數點。 在 Schema.ini 中，寬度的表示方式如下：<br /><br /> 14.083 是 FLOAT 寬度6<br /><br /> -14.083 是 FLOAT 寬度7<br /><br /> + 14.083 是 FLOAT 寬度7<br /><br /> 14083。是 FLOAT Width 6<br /><br /> ODBC 的 FLOAT 資料行一律會傳回8。<br /><br /> FLOAT 資料行也可以採用科學記號標記法，例如：<br /><br /> -3.04 e + 2 是 Float 寬度8<br /><br /> 25E4 是 Float Width 4<br /><br /> **注意** Decimal 和科學記號標記法不能混用在資料行中。<br /><br /> Null 值會以固定長度檔案中的空白填補字串表示，並在分隔檔案中省略。<br /><br /> 您可以使用前置空白填補浮點數資料。|  
|INTEGER|整數資料行的有效值為32767到-32766。<br /><br /> 在 Schema.ini 中，寬度的表示方式如下：<br /><br /> 14083為整數寬度5<br /><br /> 0是整數寬度1<br /><br /> 針對整數資料行，ODBC 一律會傳回4。<br /><br /> 最大寬度包含正負號。 整數資料行的最大寬度為11，不過寬度可能會因為固定格式資料表中允許的空白而更大。|  
|LONGCHAR|在固定長度或分隔資料表中，LONGCHAR 資料行寬度的理論限制為65500K。 文字 ISAM 更可能提供可靠的支援，最多可達32K。|  
  
 您可以在 [資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
