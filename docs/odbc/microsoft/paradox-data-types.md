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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290928"
---
# <a name="paradox-data-types"></a>Paradox 資料類型
ODBC Paradox 驅動程式會將 Paradox 資料類型對應至 ODBC SQL 資料類型。 下表列出所有 Paradox 資料類型，並顯示它們所對應的 ODBC SQL 資料類型。  
  
|Paradox 資料類型|ODBC 資料類型|  
|-----------------------|--------------------|  
|拉丁字母|SQL_VARCHAR|  
|自動遞增 [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|位元組 [1]|SQL_BINARY|  
|日期|SQL_DATE|  
|映射 [2]|SQL_LONGVARBINARY|  
|邏輯 [1]|SQL_BIT|  
|長 [1]|SQL_INTEGER|  
|備忘 [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|時間 [1]|SQL_TIMESTAMP|  
|時間戳記 [1]|SQL_TIMESTAMP|  
  
 [1] 僅對 Paradox 版本5有效。*x*。  
  
 [2] 僅適用于 Paradox 第4版。*x*和5。*x*。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**會傳回 ODBC SQL 資料類型。 本主題稍早所列的 ODBC SQL 資料類型支援 Odbc 程式設計*人員參考*附錄 D 中的所有轉換。  
  
 下表顯示 Paradox 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|拉丁字母|建立零或未指定長度的英數位中繼資料，實際上會傳回255位元組的資料行。|  
|BYTES|如果您將 Null 插入具有 Paradox5 驅動程式的二進位資料行，則會將它變更為0。|  
|LONG|Paradox 驅動程式所支援的最大負數值，其長度為5中的 LONG 資料型別。*x*不是-2 ^ 31 （-2147483648），因為長時間對應至 ODBC 資料類型 SQL_INTEGER。 Long 支援的最大負數值實際上是-2 ^ 31 + 1 （-2147483647）。|  
|timestamp|當 Paradox 驅動程式將值插入 TIMESTAMP 資料行，然後從資料行中抓取時，抓取的值可能與插入的值不同，因為四捨五入會有最多1秒的差異。|  
  
 您可以在[資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
