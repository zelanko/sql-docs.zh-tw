---
title: 使用 SQLBulkOperations 來提取資料列 |Microsoft Docs
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
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305647"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 擷取資料列
您可以透過呼叫 SQLBulkOperations，將資料根據到資料列集 **。** 要提取的資料列是由系結書簽資料行中的書簽所識別。 不會提取值為 SQL_COLUMN_IGNORE 的資料行。  
  
 若要使用**SQLBulkOperations**執行大量提取，應用程式會進行下列動作：  
  
1.  抓取並快取要更新之所有資料列的書簽。 如果使用一個以上的書簽和資料行取向系結，則會將書簽儲存在陣列中;如果使用一個以上的書簽和資料列取向系結，則會將書簽儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為要提取的資料列數目，並將包含書簽值或書簽陣列的緩衝區系結至資料行0。  
  
3.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區的 SQL_NTS 資料行的位元組長度、系結至二進位緩衝區之資料行的位元組長度，以及要設定為 Null 的任何資料行 SQL_Null_DATA。 應用程式會在要設定為預設值的資料行（如果存在的話）或 Null （如果沒有的話）中，設定要 SQL_COLUMN_IGNORE 的長度/指標緩衝區的值。  
  
4.  呼叫**SQLBulkOperations** ，並將*Operation*引數設定為 SQL_FETCH_BY_BOOKMARK。  
  
 應用程式不需要使用資料列作業陣列來防止在某些資料行上執行作業。 應用程式會選取所要提取的資料列，方法是只將這些資料列的書簽複製到系結的書簽陣列中。
