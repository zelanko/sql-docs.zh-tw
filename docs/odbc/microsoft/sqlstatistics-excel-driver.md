---
title: SQL統計(Excel 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 51b7e59fa811dd7b4ac69f1e9c8d39b4d482c437
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299338"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics (Excel 驅動程式)
> [!NOTE]  
>  本主題提供特定於 Excel 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|目錄的路徑。<br /><br /> *szTable限定符*參數不支援模式匹配。|  
|TABLE_OWNER|由於不支援擁有者名稱,因此在此列中返回 NULL。|  
|TABLE_NAME|未限制的表名稱。<br /><br /> *szTableName*參數不支援模式匹配。|  
|INDEX_QUALIFIER|NULL始終返回。|  
|INDEX_NAME|依賴於索引。|  
|TYPE|只有SQL_TABLE_STAT或SQL_INDEX_OTHER將返回 TYPE。|  
|SEQ_IN_INDEX|依賴於索引。|  
|COLUMN_NAME|依賴於索引。|  
|COLLATION|依賴於索引。|  
|PAGES|NULL始終返回。|  
  
 篩選基於唯一性 *(f唯一*參數)。 *fAccuracy*參數將被忽略。
