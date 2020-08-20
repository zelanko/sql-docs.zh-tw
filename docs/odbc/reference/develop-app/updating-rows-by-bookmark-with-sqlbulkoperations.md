---
description: 使用 SQLBulkOperations 依書籤更新資料列
title: 使用 SQLBulkOperations 依書簽更新資料列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9981136d546d53b131cff0d71edcdeab5b2e650c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482871"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤更新資料列
依書簽更新資料列時， **SQLBulkOperations** 會讓資料來源更新資料表的一或多個資料列。 這些資料列是由系結書簽資料行中的書簽所識別。 資料列會在每個系結資料行的應用程式緩衝區中使用資料進行更新 (除非資料行的長度/指標緩衝區中的值是 SQL_COLUMN_IGNORE) 。 將不會更新未系結的資料行。  
  
 若要使用 **SQLBulkOperations**以書簽來更新資料列，應用程式：  
  
1.  抓取並快取要更新之所有資料列的書簽。 如果使用多個書簽和資料行取向系結，則會將書簽儲存在陣列中;如果使用了一個以上的書簽和資料列取向的系結，則會將書簽儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為書簽的數目，並將包含書簽值的緩衝區以及書簽的陣列系結至資料行0。  
  
3.  將新的資料值放在資料列集緩衝區中。 如需有關如何使用 **SQLBulkOperations**傳送長資料的詳細資訊，請參閱 [Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區之資料行的資料或 SQL_NTS 的位元組長度、系結至二進位緩衝區的資料行之資料的位元組長度，以及要設定為 Null 之任何資料行的 SQL_Null_DATA。  
  
5.  將這些資料行的長度/指標緩衝區值設定為不會更新為 SQL_COLUMN_IGNORE 的值。 雖然應用程式可以略過此步驟並重新傳送現有的資料，但在讀取資料時，將值傳送至資料來源的風險並不高。  
  
6.  呼叫 **SQLBulkOperations** ，並將 *Operation* 引數設定為 SQL_UPDATE_BY_BOOKMARK。  
  
 針對以更新的形式傳送到資料來源的每個資料列，應用程式緩衝區應該有有效的資料列資料。 如果應用程式緩衝區是藉由提取來填滿，則如果已維護資料列狀態陣列，且如果資料列的狀態值為 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW，則不正確資料可能會不慎傳送到資料來源。
