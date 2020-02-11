---
title: 使用 SQLBulkOperations 依書簽刪除資料列 |Microsoft Docs
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
ms.openlocfilehash: a34f96dd7f5c2f0e2ac4bbb3feae06ea4856a248
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076809"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤刪除資料列
依書簽刪除資料列時， **SQLBulkOperations**會讓資料來源刪除資料表的一或多個選取資料列。 資料列是由系結的書簽資料行中的書簽所識別。  
  
 若要使用**SQLBulkOperations**以書簽刪除資料列，應用程式會執行下列動作：  
  
1.  抓取並快取要刪除的所有資料列的書簽。 如果使用一個以上的書簽和資料行取向系結，則會將書簽儲存在陣列中;如果使用一個以上的書簽和資料列取向系結，則會將書簽儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為書簽的數目，並將包含書簽值或書簽陣列的緩衝區系結至資料行0。  
  
3.  呼叫**SQLBulkOperations** ，並將*Operation*設定為 SQL_DELETE_BY_BOOKMARK。
