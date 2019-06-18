---
title: 插入資料列，使用 SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b5dac8ae14f01dd464aab42eaed42480f1e715c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446799"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>使用 SQLBulkOperations 插入資料列
使用插入資料**SQLBulkOperations**類似於更新具有資料**SQLBulkOperations**因為它會使用繫結的應用程式緩衝區的資料。  
  
 使新的資料列中的每個資料行有值，所有資料行長度/指標值為 SQL_COLUMN_IGNORE 繫結和解除繫結的所有資料行必須接受 NULL 值或具有預設值。  
  
 若要插入的資料列**SQLBulkOperations**，應用程式會進行下列作業：  
  
1.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為要插入資料列數目，並將新的資料值放在繫結的應用程式緩衝區。 如需如何將長資料與傳送**SQLBulkOperations**，請參閱[長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是 sql_nts; 之資料的繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的位元組長度。 應用程式設定的值會設為其預設值 （如果有的話） 的資料行或 SQL_COLUMN_IGNORE NULL （如果有一個不這樣做） 的長度/指標緩衝區中。  
  
3.  呼叫**SQLBulkOperations**具有*作業*引數設定為 SQL_ADD。  
  
 在後**SQLBulkOperations**傳回時，目前的資料列未變更。 如果繫結的書籤資料行 （資料行 0）， **SQLBulkOperations**傳回資料列集的緩衝區中插入的資料列的書籤繫結至該資料行。
