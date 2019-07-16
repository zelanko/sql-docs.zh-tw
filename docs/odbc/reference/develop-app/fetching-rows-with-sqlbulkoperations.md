---
title: 提取資料列，使用 SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60b6673c4a6d618e52c78b48fe7307c20c8628f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069846"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 擷取資料列
資料可以使用書籤的資料列集到 refetched 呼叫**SQLBulkOperations。** 要擷取的資料列會識別繫結的書籤資料行中的書籤。 尚未擷取的 SQL_COLUMN_IGNORE 值的資料行。  
  
 若要執行使用大量提取**SQLBulkOperations**，應用程式會進行下列作業：  
  
1.  擷取及快取要更新的所有資料列的書籤。 如果有一個以上的書籤，而且會使用資料行取向的繫結，這些書籤會儲存在陣列中;如果有一個以上的書籤，而且會使用資料列取向的繫結，這些書籤會儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為要擷取的資料列數和繫結包含書籤值或資料行 0 的書籤，陣列的緩衝區。  
  
3.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是 sql_nts; 之資料的繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的位元組長度。 應用程式設定的值會設為其預設值 （如果有的話） 的資料行或 SQL_COLUMN_IGNORE NULL （如果有一個不這樣做） 的長度/指標緩衝區中。  
  
4.  呼叫**SQLBulkOperations**具有*作業*引數設定為 SQL_FETCH_BY_BOOKMARK。  
  
 沒有要使用的資料列作業陣列，以避免作業的應用程式需要在特定資料行上執行。 應用程式，選取想要擷取到繫結的書籤的陣列複製的資料列的書籤的資料列。
