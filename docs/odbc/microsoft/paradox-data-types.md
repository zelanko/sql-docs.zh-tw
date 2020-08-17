---
description: Paradox 資料類型
title: Paradox 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44494e9945a84f978449b6bab02bd967e40d9a20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340454"
---
# <a name="paradox-data-types"></a>Paradox 資料類型
ODBC Paradox 驅動程式會將 Paradox 資料類型對應至 ODBC SQL 資料類型。 下表列出所有的 Paradox 資料類型，並顯示其所對應的 ODBC SQL 資料類型。  
  
|Paradox 資料類型|ODBC 資料類型|  
|-----------------------|--------------------|  
|字母|SQL_VARCHAR|  
|自動遞增 [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|位元組 [1]|SQL_BINARY|  
|日期|SQL_DATE|  
|影像 [2]|SQL_LONGVARBINARY|  
|邏輯 [1]|SQL_BIT|  
|LONG [1]|SQL_INTEGER|  
|備忘錄 [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|時間 [1]|SQL_TIMESTAMP|  
|時間戳記 [1]|SQL_TIMESTAMP|  
  
 [1] 只對 Paradox 版本5有效。*x*。  
  
 [2] 只對 Paradox 版本4有效。*x* 和5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 會傳回 ODBC SQL 資料類型。 本主題稍早所列的 ODBC SQL 資料類型支援 Odbc 程式設計 *人員參考* 附錄 D 中的所有轉換。  
  
 下表顯示 Paradox 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|字母|建立零或未指定長度的英數位中繼資料行，實際上會傳回255個位元組的資料行。|  
|BYTES|如果您使用 Paradox5 驅動程式將 Null 插入二進位資料行，它就會變更為0。|  
|LONG|Paradox 驅動程式在 Paradox 5 中的 LONG 資料型別所支援的最大負數值。*x* 不是-2 ^ 31 (-2147483648) ，因為它的長度對應到 ODBC 資料類型 SQL_INTEGER。 Long 所支援的最大負數值實際上是-2 ^ 31 + 1 (-2147483647) 。|  
|timestamp|當 Paradox 驅動程式將值插入時間戳記資料行，然後從資料行中取出時，從資料行中取出的值可能會與插入的值不同，因為舍入的值最多為1秒。|  
  
 您可以在 [資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
