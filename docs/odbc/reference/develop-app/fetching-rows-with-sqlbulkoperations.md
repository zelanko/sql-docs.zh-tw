---
description: 使用 SQLBulkOperations 擷取資料列
title: 使用 SQLBulkOperations 提取資料列 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4c3cb6a38e3ef9c42f4e853b8c406579b5c0236
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499868"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 擷取資料列
您可以透過呼叫 SQLBulkOperations，使用書簽將資料根據至資料列集 **。** 要提取的資料列是由系結書簽資料行中的書簽所識別。 未提取值為 SQL_COLUMN_IGNORE 的資料行。  
  
 若要使用 **SQLBulkOperations**執行大量提取，應用程式會執行下列動作：  
  
1.  抓取並快取要更新之所有資料列的書簽。 如果使用多個書簽和資料行取向系結，則會將書簽儲存在陣列中;如果使用了一個以上的書簽和資料列取向的系結，則會將書簽儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為要提取的資料列數目，並將包含書簽值的緩衝區以及書簽的陣列系結至資料行0。  
  
3.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區之資料行的資料或 SQL_NTS 的位元組長度、系結至二進位緩衝區的資料行之資料的位元組長度，以及要設定為 Null 之任何資料行的 SQL_Null_DATA。 應用程式會將這些資料行的長度/指標緩衝區中的值設定為其預設 (（如果有的話）) 或 Null (如果沒有) SQL_COLUMN_IGNORE 的話）。  
  
4.  呼叫 **SQLBulkOperations** ，並將 *Operation* 引數設定為 SQL_FETCH_BY_BOOKMARK。  
  
 應用程式不需要使用資料列作業陣列來防止在特定資料行上執行作業。 應用程式會藉由只將這些資料列的書簽複製到系結的書簽陣列中，來選取要提取的資料列。
