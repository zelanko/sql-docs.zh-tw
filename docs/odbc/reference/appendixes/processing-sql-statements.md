---
title: 處理 SQL 語句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9452ade90f6967dff6d72d5692efcf91b93154d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057239"
---
# <a name="processing-sql-statements"></a>處理 SQL 陳述式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 ODBC 資料指標程式庫會將所有的 SQL 語句直接傳遞到驅動程式，但下列除外：  
  
-   定位 update 和 delete 語句  
  
-   **針對 UPDATE 語句選取**  
  
-   批次 SQL 語句  
  
 若要執行定位的 update 和 delete 語句，並將資料指標置於資料列上，以呼叫該資料列的**SQLGetData** ，資料指標程式庫會建立可識別該資料列的搜尋語句。  
  
 此章節包含下列主題。  
  
-   [處理定點更新和刪除陳述式](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [處理 SELECT FOR UPDATE 陳述式](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [批次處理 SQL 陳述式](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)
