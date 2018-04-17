---
title: 提取資料列 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 81fff470f916155e9b6d85571db46c46d9e63454
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-a-row-of-data"></a>提取資料列
若要擷取的資料列，應用程式呼叫**SQLFetch**。 **SQLFetch**可以使用任何一種資料指標，呼叫，但它只會以順向方向移動資料列集資料指標。 **SQLFetch**游標前進到下一個資料列，並傳回已繫結呼叫的任何資料行的資料**SQLBindCol**。 設定資料指標時達到結果的結尾， **SQLFetch**傳回 sql_no_data 為止。 如需呼叫的範例**SQLFetch**，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 方式**SQLFetch**實作驅動程式特有的但是一般模式是讓擷取資料的任何資料行繫結資料來源，將它根據繫結的變數、 類型轉換，並設定驅動程式轉換中這些變數的詳細資料。 如果驅動程式無法轉換任何資料， **SQLFetch**會傳回錯誤。 應用程式可以繼續提取資料列，但目前的資料列的資料都會遺失。 未繫結的資料行的資料會發生什麼事取決於驅動程式，但大多數的驅動程式擷取並捨棄它或永遠不會進行擷取。  
  
 驅動程式也會設定已繫結任何長度/指標緩衝區的值。 如果資料行的資料值為 NULL，則驅動程式會設定對應的長度/指標緩衝區為 SQL_NULL_DATA。 如果資料值不是 NULL，則驅動程式會設定為資料的位元組長度之長度/指標緩衝區轉換後。 如果無法判別此長度，因為有時候是使用一個以上的函式呼叫所擷取的長資料的情況下，驅動程式會將長度/指標緩衝區設 SQL_NO_TOTAL。 固定長度資料類型，包括像是整數和日期結構的位元組長度會是資料類型的大小。  
  
 可變長度的資料，例如字元和二進位資料時，驅動程式會檢查已轉換的資料，針對資料行，來繫結之緩衝區的位元組長度的位元組長度中指定的緩衝區長度*Columnsize*引數中的**SQLBindCol**。 如果已轉換資料的位元組長度大於緩衝區的位元組長度，驅動程式截斷以符合緩衝區中的資料，傳回未截斷的長度之長度/指標緩衝區，以傳回 SQL_SUCCESS_WITH_INFO，並將 SQLSTATE 01004 （資料在診斷中截斷）。 唯一的例外是如果在傳回時，截斷可變長度的書籤**SQLFetch**，它會傳回 SQLSTATE 22001 （字串資料，右邊已截斷）。  
  
 永遠不會截斷固定長度的資料，因為驅動程式會假設繫結緩衝區的大小是資料類型的大小。 資料截斷通常會很少見，因為應用程式通常會繫結緩衝區不夠大，無法儲存整個資料值;它會判斷從中繼資料所需的大小。 不過，應用程式可能會明確繫結的緩衝區，它知道太小。 比方說，它可能會擷取並顯示組件描述的前 20 個字元或長文字資料行的前 100 個字元。  
  
 字元資料必須先以 null 結束的驅動程式傳回至應用程式，即使它已被截斷。 Null 結束的字元不會包含在傳回的位元組長度，但需要繫結緩衝區的空間。 例如，假設應用程式使用 ASCII 字元集中的字元資料所組成的字串、 驅動程式有 50 個字元的要傳回的資料和應用程式的緩衝區是長度為 25 個位元組。 在應用程式的緩衝區，驅動程式會傳回後面 null 結束字元的第一次 24 個字元。 在長度/指標緩衝區，它會傳回位元組長度為 50。  
  
 應用程式可以限制結果集之前執行的陳述式，建立結果集，設定 SQL_ATTR_MAX_ROWS 陳述式屬性中的資料列數目。 例如，應用程式用來格式化報表中的預覽模式需要只資料不足，無法顯示報表的第一頁。 藉由限制結果集的大小，此類功能就會執行更快。 此陳述式屬性為了降低網路流量，並可能不支援所有的驅動程式。
