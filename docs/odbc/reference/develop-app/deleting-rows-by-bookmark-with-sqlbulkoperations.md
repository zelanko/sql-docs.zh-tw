---
title: 刪除資料列的書籤使用 SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5895a106c389afe2d1979cf8d9c16e92f570538a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849456"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤刪除資料列
當刪除資料列的書籤**SQLBulkOperations**刪除一或多個選取的資料列之資料表的資料來源。 資料列識別的繫結的書籤資料行中的書籤。  
  
 若要刪除資料列具有書籤**SQLBulkOperations**，應用程式會進行下列作業：  
  
1.  擷取及快取要刪除的所有資料列的書籤。 如果有一個以上的書籤，而且會使用資料行取向的繫結，這些書籤會儲存在陣列中;如果有一個以上的書籤，而且會使用資料列取向的繫結，這些書籤會儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為書籤的數目並繫結包含書籤值或資料行 0 的書籤，陣列的緩衝區。  
  
3.  呼叫**SQLBulkOperations**具有*作業*設 SQL_DELETE_BY_BOOKMARK。
