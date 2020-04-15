---
title: 悖論資料類型 |微軟文件
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
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290928"
---
# <a name="paradox-data-types"></a>Paradox 資料類型
ODBC 悖論驅動程式將悖論數據類型映射到 ODBC SQL 數據類型。 下表列出了所有 Paradox 資料類型,並顯示了對應到的 ODBC SQL 資料類型。  
  
|已悖論資料類型|ODBC 資料類型|  
|-----------------------|--------------------|  
|字母|SQL_VARCHAR|  
|自動遞增[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|位元組[1]|SQL_BINARY|  
|日期|SQL_DATE|  
|圖片[2]|SQL_LONGVARBINARY|  
|邏輯[1]|SQL_BIT|  
|長[1]|SQL_INTEGER|  
|備忘錄[2]|SQL_LONGVARCHAR|  
|錢[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|時間[1]|SQL_TIMESTAMP|  
|時間戳[1]|SQL_TIMESTAMP|  
  
 [1] 僅適用於悖論版本 5。*x*. .  
  
 [2] 僅適用於悖論版本 4。*x*和 5。*x*. .  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 本主題前面列出的 ODBC SQL 資料類型都支援*ODBC 程式師參考*附錄 D 中的所有轉換。  
  
 下表顯示了對悖論數據類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|字母|創建零或未指定長度的 ALPHA 數位列實際上返回 255 位元組列。|  
|BYTES|如果將 NULL 插入具有 Paradox5 驅動程式的二進位列中,則它將更改為 0。|  
|LONG|悖論 5 中長數據類型的悖論驅動程式支援的最大負值。*x*不是 -2^31 (-2147483648),因為它應該是因為長映射到 ODBC 數據類型SQL_INTEGER。 Long 支援的最大負值實際上是 -2^31 = 1 (-2147483647)。|  
|timestamp|當一個值被 Paradox 驅動程式插入到 TIMESTAMP 列中,然後從該列檢索時,檢索的值可能與插入的值相差 1 秒,因為捨入。|  
  
 數據類型的更多限制可以在[數據類型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
