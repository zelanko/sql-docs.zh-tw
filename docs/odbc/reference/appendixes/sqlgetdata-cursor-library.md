---
title: SQLGetData （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b9f9f3217e455d523cbf0740531b5a3c88d1720
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetData**資料指標程式庫中的函式。 如需一般資訊**SQLGetData**，請參閱[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 資料指標程式庫實作**SQLGetData**首先透過建構**選取**陳述式搭配**其中**列舉的值儲存在每個繫結其快取中的子句目前的資料列中的資料行。 接著它會執行**選取**陳述式以重新選取資料列和呼叫**SQLGetData**驅動程式 （相對於快取） 資料來源擷取資料中。  
  
> [!CAUTION]  
>  **其中**子句所識別的目前資料列的資料指標程式庫建構無法識別任何資料列、 識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱[建構搜尋陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE， **SQLGetData**可以呼叫資料行 0 傳回書籤的資料。  
  
 呼叫**SQLGetData**受限於下列限制：  
  
-   **SQLGetData**無法呼叫順向資料指標。  
  
-   **SQLGetData**符合下列條件時，才可以呼叫：**選取**陳述式產生結果集;**選取**陳述式未包含聯結， **等位**子句，或**GROUP BY**子句; 和選取清單中使用的別名或運算式的任何資料行未繫結與**SQLBindCol**。  
  
-   如果驅動程式支援只有一個使用中陳述式，資料指標程式庫會提取結果集之前執行的 rest**選取**陳述式，並呼叫**SQLGetData**。
