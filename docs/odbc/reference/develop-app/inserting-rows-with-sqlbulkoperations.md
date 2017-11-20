---
title: "插入資料列與 SQLBulkOperations |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd79255e4cda68d1fd4d425544702e589f44336b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="inserting-rows-with-sqlbulkoperations"></a>插入 SQLBulkOperations 具有資料列
使用插入資料**SQLBulkOperations**類似於更新具有資料**SQLBulkOperations**因為它會使用資料繫結應用程式緩衝區。  
  
 使新的資料列中的每個資料行有值，所有繫結的資料行長度/指標值是 SQL_COLUMN_IGNORE 和未繫結的所有資料行必須接受 NULL 值或具有預設值。  
  
 若要插入的資料列**SQLBulkOperations**，應用程式會進行下列作業：  
  
1.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為要插入資料列數目，並將新的資料值放在繫結應用程式緩衝區中。 如需有關如何以傳送長資料與詳細**SQLBulkOperations**，請參閱[Long 資料和 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的資料或 SQL_NTS 的位元組長度。 應用程式設定的值會設為其預設值 （如果有的話） 的資料行或 SQL_COLUMN_IGNORE NULL （如果其中一個不存在） 的長度/指標緩衝區中。  
  
3.  呼叫**SQLBulkOperations**與*作業*引數設定為 SQL_ADD。  
  
 之後**SQLBulkOperations**傳回目前的資料列不會變更。 如果書籤資料行 （資料行 0） 會繫結， **SQLBulkOperations**傳回資料列集的緩衝區中插入的資料列的書籤繫結至該資料行。

