---
description: 使用 SQLBulkOperations 依書籤刪除資料列
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dcb96180cdcee5987d8a1cbafeae117ec82bba0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424680"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤刪除資料列
依書簽刪除資料列時， **SQLBulkOperations** 會讓資料來源刪除資料表的一或多個選取的資料列。 這些資料列是由系結書簽資料行中的書簽所識別。  
  
 若要使用 **SQLBulkOperations**以書簽刪除資料列，應用程式會執行下列動作：  
  
1.  抓取並快取所有要刪除之資料列的書簽。 如果使用多個書簽和資料行取向系結，則會將書簽儲存在陣列中;如果使用了一個以上的書簽和資料列取向的系結，則會將書簽儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為書簽的數目，並將包含書簽值的緩衝區以及書簽的陣列系結至資料行0。  
  
3.  呼叫 **SQLBulkOperations** ，並將 *Operation* 設定為 SQL_DELETE_BY_BOOKMARK。
