---
title: 處理 SQL 語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eda640f6e810eeccbfa17ea2b6ba7c1b19b28e08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307999"
---
# <a name="processing-sql-statements"></a>處理 SQL 陳述式
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 ODBC 游標庫將所有 SQL 語句直接傳遞給驅動程式,但以下情況除外:  
  
-   請找到更新與移除敘述  
  
-   **選擇更新**敘述  
  
-   批次 SQL 語句  
  
 要執行定位更新和刪除語句,並將游標放置在行上以調用該行的**SQLGetData,** 遊標庫將建構標識該行的搜索語句。  
  
 此章節包含下列主題。  
  
-   [處理定位的 Update 和 Delete 陳述式](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [處理 SELECT FOR UPDATE 陳述式](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 陳述式的處理批次](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)
