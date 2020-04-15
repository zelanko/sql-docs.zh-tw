---
title: SQL統計(存取驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299358"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|返回資料庫檔的路徑以用於Microsoft Access。<br /><br /> *szTable限定符*參數不支援模式匹配。|  
|TABLE_OWNER|NULL 在此列中返回,因為不支援所有者名稱。|  
|TABLE_NAME|未限制的表名稱。<br /><br /> *szTableName*參數不支援模式匹配。|  
|INDEX_QUALIFIER|NULL始終返回。|  
|INDEX_NAME|依賴於索引。|  
|TYPE|只有SQL_TABLE_STAT或SQL_INDEX_OTHER將返回 TYPE。|  
|SEQ_IN_INDEX|依賴於索引。|  
|COLUMN_NAME|依賴於索引。|  
|COLLATION|依賴於索引。|  
|CARDINALITY|僅為 Microsoft 訪問返回。|  
|PAGES|NULL始終返回。|  
  
 篩選基於唯一性 *(f唯一*參數)。 *fAccuracy*參數將被忽略。
