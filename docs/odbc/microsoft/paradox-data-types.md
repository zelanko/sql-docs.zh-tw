---
title: "Paradox 資料型別 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40266f580e162ed021c069c1b583748906b3b336
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="paradox-data-types"></a>Paradox 資料類型
ODBC Paradox 驅動程式會將 Paradox 資料類型對應至 ODBC SQL 資料類型。 下表列出所有 Paradox 資料型別，並顯示 ODBC SQL 資料類型對應至。  
  
|Paradox 資料類型|ODBC 資料類型|  
|-----------------------|--------------------|  
|英數字元|SQL_VARCHAR|  
|自動遞增 [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|位元組 [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|影像 [2]|SQL_LONGVARBINARY|  
|邏輯 [1]|SQL_BIT|  
|長時間 [1]|SQL_INTEGER|  
|附註 [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|短|SQL_SMALLINT|  
|時間 [1]|SQL_TIMESTAMP|  
|時間戳記 [1]|SQL_TIMESTAMP|  
  
 僅針對 Paradox 版本 5 的有效 [1]。*x*。  
  
 [2] 適只用於 Paradox 4 版。*x*和 5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 所有的轉換中的 < 附錄 D *ODBC 程式設計人員參考*支援本主題稍早所列的 ODBC SQL 資料類型。  
  
 下表顯示 Paradox 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|英數字元|建立的英數字元的資料行的零或未指定的長度實際上會傳回 255 個位元組的資料行。|  
|BYTES|如果您將 NULL 插入 Paradox5 驅動程式的二進位資料行時，會將它變更為 0。|  
|LONG|Long 資料類型的 Paradox 5 Paradox 驅動程式支援的最大負數值。*x*不是-2 ^31 (-2147483648)，因為很長的對應至 ODBC 資料之後輸入 SQL_INTEGER。 支援長時間的最大負數的值為實際上-2 ^31 + 1 (-2147483647)。|  
|timestamp|當值插入 TIMESTAMP 資料行中的 Paradox 驅動程式，則接著就會擷取從資料行時，擷取的值可能不同於插入的值最多可達 1 的第二個因為捨入。|  
  
 資料類型的多個限制可以在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。
