---
title: SQLStatistics （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 634fbcdbf78515e59295e679072ffa5fd08e4823
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686929"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|「資料行」|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|目錄的路徑。<br /><br /> 模式比對中不支援*szTableQualifier*引數。|  
|TABLE_OWNER|在本專欄中會傳回 NULL，因為不支援擁有者名稱。|  
|TABLE_NAME|分隔的資料表名稱。<br /><br /> 模式比對中不支援*szTableName*引數。|  
|INDEX_QUALIFIER|永遠傳回 NULL。|  
|INDEX_NAME|索引相關。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 就會傳回型別。|  
|SEQ_IN_INDEX|索引相關。|  
|COLUMN_NAME|索引相關。|  
|COLLATION|索引相關。|  
|PAGES|永遠傳回 NULL。|  
  
 篩選根據唯一性 ( *fUnique*引數)。 *FAccuracy*參數會被忽略。
