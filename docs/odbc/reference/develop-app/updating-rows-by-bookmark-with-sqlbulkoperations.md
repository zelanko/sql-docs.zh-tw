---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9b10037883ef9cfa4051195270e6477c5cc04ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091617"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤更新資料列
依書簽更新資料列時， **SQLBulkOperations**會讓資料來源更新資料表的一或多個資料列。 資料列是由系結的書簽資料行中的書簽所識別。 在每個系結資料行的應用程式緩衝區中，會使用資料來更新該資料列（但當資料行的長度/指標緩衝區中的值是 SQL_COLUMN_IGNORE 時除外）。 未系結的資料行將不會更新。  
  
 若要使用**SQLBulkOperations**，以書簽更新資料列，應用程式：  
  
1.  抓取並快取要更新之所有資料列的書簽。 如果使用一個以上的書簽和資料行取向系結，則會將書簽儲存在陣列中;如果使用一個以上的書簽和資料列取向系結，則會將書簽儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為書簽的數目，並將包含書簽值或書簽陣列的緩衝區系結至資料行0。  
  
3.  將新的資料值放在資料列集緩衝區中。 如需有關如何使用**SQLBulkOperations**傳送長資料的詳細資訊，請參閱[冗長資料和 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區的 SQL_NTS 資料行的位元組長度、系結至二進位緩衝區之資料行的位元組長度，以及要設定為 Null 的任何資料行 SQL_Null_DATA。  
  
5.  將這些資料行的長度/指標緩衝區中的值設定為不會更新為 SQL_COLUMN_IGNORE。 雖然應用程式可以略過此步驟並重新傳送現有資料，但這種情況沒有效率，而且會在讀取資料時將值傳送到已截斷的資料來源。  
  
6.  呼叫**SQLBulkOperations** ，並將*Operation*引數設定為 SQL_UPDATE_BY_BOOKMARK。  
  
 針對傳送至資料來源做為更新的每個資料列，應用程式緩衝區應該具有有效的資料列資料。 如果應用程式緩衝區已藉由提取填滿，如果已維護資料列狀態陣列，而且資料列的狀態值是 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW，則不正確資料可能會不小心傳送至資料來源。
