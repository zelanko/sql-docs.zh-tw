---
title: 索引鍵集驅動資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c40fe8c823115c3131a1719185bce8f1506df81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138836"
---
# <a name="keyset-driven-cursors"></a>索引鍵集導向的資料指標
索引鍵集驅動資料指標的靜態和動態資料指標之間在於它能夠偵測變更。 如同靜態資料指標，它不一定會偵測結果集的成員資格和順序變更。 動態資料指標，例如它沒有偵測到值的資料列的變更結果集中 （受限於 SQL_ATTR_TXN_ISOLATION 連接屬性所設定的交易隔離等級）。  
  
 索引鍵集驅動資料指標開啟時，它會將儲存整個結果集，則索引的鍵這會修正的明顯的成員資格和順序的結果集。 當資料指標捲動透過結果集時，它會使用該索引鍵以此*keyset*來擷取目前的資料值，每個資料列。 例如，假設的索引鍵集驅動資料指標提取資料列和另一個應用程式，然後更新該資料列。 如果資料指標 refetches 資料列，它所看到的值會是新的因為它 refetched 使用它的索引鍵的資料列。 因為這個緣故，索引鍵集驅動資料指標一律會偵測本身與其他人所做的變更。  
  
 資料指標會嘗試擷取已刪除的資料列，這個資料列會顯示為結果集內的 「 漏洞 」:索引鍵集中存在資料列的索引鍵，但結果集中不再有此資料列。 如果已更新資料列中的索引鍵值，資料列視為已刪除，然後插入，因此這類資料列也會顯示為結果集中的漏洞。 雖然索引鍵集驅動資料指標一律可以偵測到其他人所刪除的資料列，它可以選擇性地移除索引鍵的資料列會自行從刪除索引鍵集。 執行這項操作的索引鍵集驅動資料指標無法偵測到自己刪除。 特定的索引鍵集驅動資料指標是否偵測到它自己刪除透過 SQL_STATIC_SENSITIVITY 選項中會回報**SQLGetInfo**。  
  
 因為這些資料列的任何索引鍵不存在於索引鍵集，會永遠不會顯示給索引鍵集驅動資料指標的其他人所插入的資料列。 不過，索引鍵集驅動資料指標可以選擇性地加入索引鍵的資料列插入本身以索引鍵集。 執行這項操作的索引鍵集驅動資料指標可以偵測到他們自己插入。 特定的索引鍵集驅動資料指標是否偵測到它自己插入透過 SQL_STATIC_SENSITIVITY 選項中會回報**SQLGetInfo**。  
  
 Sql_attr_row_status_ptr 設定陳述式屬性所指定之資料列狀態陣列可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 的任何資料列。 它會傳回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或 SQL_ROW_ADDED 它偵測為已更新的資料列刪除或插入。  
  
 索引鍵集驅動資料指標通常會實作藉由建立暫存資料表，其中包含在結果集中的每個資料列的索引鍵。 資料指標也必須決定是否已更新資料列，因為此資料表通常也會包含具有資料列版本設定資訊的資料行。  
  
 若要捲動原始結果集，索引鍵集驅動資料指標會開啟靜態資料指標放在暫存表格。 若要擷取原始的結果集中資料列，資料指標第一次從暫存資料表中擷取適當的索引鍵，並接著會擷取資料列的目前值。 如果使用區塊資料指標時，游標必須擷取多個索引鍵和資料列。
