---
description: 處理 SQL 陳述式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 381bb7bbc27fc74b5d57fbb01b6a80f17305f5cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483186"
---
# <a name="processing-sql-statements"></a>處理 SQL 陳述式
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 ODBC 資料指標程式庫會將所有 SQL 語句直接傳遞至驅動程式，但下列情況除外：  
  
-   定位的 update 和 delete 語句  
  
-   **SELECT FOR UPDATE** 語句  
  
-   批次 SQL 語句  
  
 若要執行定位的 update 和 delete 語句，以及將資料指標置於資料列上，以呼叫該資料列的 **SQLGetData** ，資料指標程式庫會建立識別資料列的搜尋語句。  
  
 此章節包含下列主題。  
  
-   [處理定位的 Update 和 Delete 陳述式](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [處理 SELECT FOR UPDATE 陳述式](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 陳述式的處理批次](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)
