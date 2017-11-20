---
title: "索引鍵集驅動資料指標 |Microsoft 文件"
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
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7cbd7ca159b09ee1482139ef76bfff48115a62bd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="keyset-driven-cursors"></a>索引鍵集驅動資料指標
索引鍵集驅動資料指標的介於靜態和動態資料指標偵測變更的能力。 類似靜態資料指標，它不一定偵測的變更的成員資格和順序的結果集。 動態資料指標，例如它沒有結果集 （受限於由 SQL_ATTR_TXN_ISOLATION 連接屬性設定的交易隔離等級） 來偵測變更的資料列的值。  
  
 索引鍵集驅動資料指標開啟時，它會將儲存的索引鍵的整個結果集;這會修正的明顯的成員資格和順序的結果集。 資料指標捲動的結果集，因為它會使用該索引鍵在這個*索引鍵集*擷取目前的資料值，每個資料列。 例如，假設的索引鍵集驅動資料指標提取的資料列，而另一個應用程式，然後再更新該資料列。 如果資料指標 refetches 資料列，它看見的值會是新的因為它 refetched 使用它的索引鍵的資料列。 因為這個緣故，索引鍵集驅動資料指標一律會偵測本身和其他人所做的變更。  
  
 當游標嘗試擷取已刪除的資料列時，這個資料列會顯示為結果集中的 「 洞": 資料列的索引鍵存在於索引鍵集，但該資料列不再存在於結果集。 如果已更新的索引鍵值的資料列中，資料列會被視為已刪除，然後插入，因此這類資料列也會顯示為結果集中的漏洞。 雖然索引鍵集驅動資料指標一律可以偵測到其他人所刪除的資料列，它可以選擇性地移除索引鍵的資料列刪除本身從索引鍵集。 執行此動作的索引鍵集驅動資料指標偵測不到他們自己的刪除。 特定的索引鍵集驅動資料指標是否偵測到它自己的刪除動作會報告透過 SQL_STATIC_SENSITIVITY 選項中**SQLGetInfo**。  
  
 因為未針對這些資料列的索引鍵存在於索引鍵集，會永遠不會顯示索引鍵集驅動資料指標給其他人所插入的資料列。 不過，索引鍵集驅動資料指標可以選擇性地加入索引鍵的資料列它本身對插入索引鍵集。 執行此動作的索引鍵集驅動資料指標可以偵測到自己的插入。 透過 SQL_STATIC_SENSITIVITY 選項中為報告的特定索引鍵集驅動資料指標是否偵測到它自己的插入**SQLGetInfo**。  
  
 將 sql_attr_row_status_ptr 設定陳述式屬性所指定之資料列狀態陣列可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 的任何資料列。 它會傳回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或 SQL_ROW_ADDED 它偵測為更新的資料列的刪除或插入。  
  
 索引鍵集驅動資料指標通常會實作所建立的暫存資料表，其中包含在結果集中的每個資料列的索引鍵。 資料指標也必須決定是否已更新資料列，因為此資料表也通常會包含具有資料列版本設定資訊的資料行。  
  
 若要捲動原始結果集，索引鍵集驅動資料指標會開啟靜態資料指標放在暫存表格。 若要擷取的原始結果集中的資料列，資料指標從暫存資料表會先擷取適當的索引鍵，並接著會擷取資料列的目前值。 如果使用區塊資料指標時，游標必須擷取多個索引鍵和資料列。

