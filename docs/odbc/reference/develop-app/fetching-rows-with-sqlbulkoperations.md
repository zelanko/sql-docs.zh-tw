---
title: 提取資料列與 SQLBulkOperations |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2481fe60919a120c0e286c6b7bf3554923bdd0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>提取資料列與 SQLBulkOperations
資料可以使用書籤的資料列集到 refetched 呼叫**SQLBulkOperations。** 要讀取的資料列會識別繫結的書籤資料行中的書籤。 不會擷取具有 SQL_COLUMN_IGNORE 值的資料行。  
  
 若要執行使用大量擷取**SQLBulkOperations**，應用程式會進行下列作業：  
  
1.  擷取和快取要更新的所有資料列的書籤。 如果有多個書籤，並且使用資料行取向的繫結，這些書籤會儲存在陣列;如果有多個書籤，並且使用資料列取向的繫結，這些書籤會儲存在資料列結構的陣列。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為要擷取的資料列數目，並繫結包含書籤值或資料行 0 的書籤，陣列的緩衝區。  
  
3.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的資料或 SQL_NTS 的位元組長度。 應用程式設定的值會設為其預設值 （如果有的話） 的資料行或 SQL_COLUMN_IGNORE NULL （如果其中一個不存在） 的長度/指標緩衝區中。  
  
4.  呼叫**SQLBulkOperations**與*作業*引數設定為 SQL_FETCH_BY_BOOKMARK。  
  
 沒有要使用的資料列作業陣列，以避免作業的應用程式需要在特定資料行上執行。 應用程式選取要繫結的書籤陣列中複製這些資料列的書籤提取資料的列。
