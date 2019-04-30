---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2f3b1e63578af7c0b42f00113fbb9e87cb8003
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208422"
---
# <a name="paradox-data-types"></a>Paradox 資料類型
ODBC Paradox 驅動程式會將 Paradox 資料類型對應至 ODBC SQL 資料類型。 下表列出所有 Paradox 資料類型，並顯示 ODBC SQL 資料類型，它們會對應至。  
  
|Paradox 資料類型|ODBC 資料類型|  
|-----------------------|--------------------|  
|英數字元|SQL_VARCHAR|  
|AUTOINCREMENT[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTES[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGE[2]|SQL_LONGVARBINARY|  
|LOGICAL[1]|SQL_BIT|  
|LONG[1]|SQL_INTEGER|  
|MEMO[2]|SQL_LONGVARCHAR|  
|MONEY[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|簡短|SQL_SMALLINT|  
|TIME[1]|SQL_TIMESTAMP|  
|TIMESTAMP[1]|SQL_TIMESTAMP|  
  
 [1] 只會針對 Paradox 第 5 版的有效。*x*。  
  
 [2] 的適僅用於 Paradox 版本 4。*x*和 5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 附錄 D 中的所有轉換*ODBC 程式設計人員參考*稍早在本主題中列出的 ODBC SQL 資料類型支援。  
  
 下表顯示 Paradox 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|英數字元|建立的英數字元的資料行的零或未指定的長度實際上會傳回 255 個位元組的資料行。|  
|BYTES|如果您將 NULL 插入 Paradox5 驅動程式的二進位資料行時，會將它變更為 0。|  
|LONG|Paradox 5 中的 Long 資料類型的 Paradox 驅動程式所支援的最大負數值。*x*不是-2 ^31 (-2147483648)，因為它應該是因為長時間對應至 ODBC 資料類型 SQL_INTEGER。 支援長時間的最大負數的值是實際上-2 ^31 + 1 (-2147483647)。|  
|timestamp|當值是 Paradox 驅動程式插入時間戳記資料行，再接著就會擷取從資料行時，擷取的值可能不同於插入的值最高達 1 的第二個因為捨入。|  
  
 資料型別上的更多限制可在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。
