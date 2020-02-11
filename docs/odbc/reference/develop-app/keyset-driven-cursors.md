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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138836"
---
# <a name="keyset-driven-cursors"></a>索引鍵集導向的資料指標
索引鍵集驅動資料指標位於靜態和動態資料指標之間，其偵測變更的能力。 如同靜態資料指標，它不一定會偵測結果集的成員資格和順序變更。 就像動態資料指標一樣，它會偵測結果集中資料列值的變更（受 SQL_ATTR_TXN_ISOLATION 連接屬性所設定的交易隔離等級所需）。  
  
 當索引鍵集驅動資料指標開啟時，它會儲存整個結果集的索引鍵。這會修正結果集的明顯成員資格和順序。 當資料指標滾動到結果集時，它會使用這個索引鍵集中的索引*鍵來抓取*每個資料列的目前資料值。 例如，假設索引鍵集驅動資料指標提取資料列，另一個應用程式則會更新該資料列。 如果資料指標 refetches 資料列，它會看到的值是新的，因為它會使用索引鍵來根據資料列。 因此，索引鍵集導向的資料指標一律會偵測本身和其他人所做的變更。  
  
 當資料指標嘗試抓取已刪除的資料列時，這個資料列會在結果集中顯示為「洞」：資料列的索引鍵存在於索引鍵集中，但資料列已不存在於結果集內。 如果資料列中的索引鍵值已更新，則會將資料列視為已刪除然後插入，因此這類資料列也會顯示為結果集中的洞。 雖然索引鍵集驅動資料指標永遠可以偵測到其他人所刪除的資料列，但它可以選擇性地移除索引鍵，以供它從索引鍵集刪除本身的資料列。 執行此動作的索引鍵集驅動資料指標無法偵測自己的刪除。 特定索引鍵集驅動資料指標是否會偵測其本身的刪除，會透過**SQLGetInfo**中的 [SQL_STATIC_SENSITIVITY] 選項來回報。  
  
 索引鍵集驅動資料指標不會看到其他人所插入的資料列，因為索引鍵集中不存在這些資料列的索引鍵。 不過，索引鍵集驅動資料指標可以選擇性地加入其本身插入索引鍵集中的資料列索引鍵。 執行此動作的索引鍵集驅動資料指標可以偵測自己的插入。 特定索引鍵集驅動資料指標是否會偵測到自己的插入，是透過**SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 選項來回報。  
  
 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定的資料列狀態陣列可以包含任何資料列的 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR。 它會針對它偵測為更新、刪除或插入的資料列，傳回 SQL_ROW_UPDATED、SQL_ROW_DELETED 或 SQL_ROW_ADDED。  
  
 索引鍵集驅動資料指標通常是藉由建立一個臨時表，其中包含結果集中每個資料列的索引鍵來執行。 因為資料指標也必須判斷是否已更新資料列，所以此資料表通常也會包含具有資料列版本設定資訊的資料行。  
  
 若要在原始結果集上滾動，索引鍵集驅動資料指標會開啟臨時表上的靜態資料指標。 若要取出原始結果集中的資料列，資料指標會先從臨時表中抓取適當的索引鍵，然後再抓取資料列的目前值。 如果使用區塊資料指標，則游標必須取出多個索引鍵和資料列。
