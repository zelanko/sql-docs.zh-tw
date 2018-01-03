---
title: "刪除具有 SQLBulkOperations 書籤的資料列 |Microsoft 文件"
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
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb572386d385ea081297bc752a9c0f1dd9a8fd7b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>刪除具有 SQLBulkOperations 書籤的資料列
當刪除資料列的書籤， **SQLBulkOperations** ，使得資料來源刪除一或多個選取的資料列的資料表。 資料列識別的繫結的書籤資料行中的書籤。  
  
 若要刪除資料列具有書籤**SQLBulkOperations**，應用程式會進行下列作業：  
  
1.  擷取和快取要刪除的所有資料列的書籤。 如果有多個書籤，並且使用資料行取向的繫結，這些書籤會儲存在陣列;如果有多個書籤，並且使用資料列取向的繫結，這些書籤會儲存在資料列結構的陣列。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為書籤的數目，並繫結包含書籤值或資料行 0 的書籤，陣列的緩衝區。  
  
3.  呼叫**SQLBulkOperations**與*作業*設 SQL_DELETE_BY_BOOKMARK。
