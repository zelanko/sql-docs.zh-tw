---
description: 索引鍵集導向的資料指標
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c34432481eeafd6bed938dcd1275e33583d33cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476590"
---
# <a name="keyset-driven-cursors"></a>索引鍵集導向的資料指標
索引鍵集驅動的資料指標存在於靜態和動態資料指標，以偵測變更的能力。 如同靜態資料指標，它不一定會偵測結果集的成員資格和順序變更。 和動態資料指標一樣，它會偵測結果集中的資料列值變更 (受限於 SQL_ATTR_TXN_ISOLATION 連接屬性) 所設定的交易隔離等級。  
  
 當索引鍵集驅動資料指標開啟時，它會儲存整個結果集的索引鍵;這會修正結果集的明顯成員資格和順序。 當資料指標滾動整個結果集時，它會 *使用此索引鍵集中* 的索引鍵，來取得每個資料列的目前資料值。 例如，假設索引鍵集驅動資料指標提取資料列，然後另一個應用程式會更新該資料列。 如果資料指標 refetches 資料列，它會看到新的值，因為它會使用索引鍵來根據資料列。 因此，索引鍵集驅動的資料指標一律會偵測本身和其他的變更。  
  
 當資料指標嘗試抓取已刪除的資料列時，此資料列會在結果集中顯示為「洞」：資料列的索引鍵存在於索引鍵集中，但資料列已不存在於結果集中。 如果資料列中的索引鍵值已更新，資料列就會被視為已刪除然後插入，因此這類資料列也會顯示為結果集中的漏洞。 當索引鍵集驅動的資料指標一律可以偵測其他人刪除的資料列時，可以選擇性地從索引鍵集移除其本身所刪除之資料列的索引鍵。 這樣做的索引鍵集驅動資料指標無法偵測到它們自己的刪除。 特定索引鍵集驅動的資料指標是否會偵測到它自己的刪除，會透過 **SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 選項回報。  
  
 在索引鍵集驅動的資料指標上，不會看到其他人所插入的資料列，因為這些資料列的索引鍵不存在於索引鍵集中。 不過，索引鍵集驅動的資料指標可以選擇性地加入資料列的索引鍵，其會將其插入至索引鍵集。 這樣做的索引鍵集驅動資料指標，可以偵測自己的插入。 特定索引鍵集導向的資料指標是否會透過 **SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 選項回報自己的插入。  
  
 SQL_ATTR_ROW_STATUS_PTR 語句屬性指定的資料列狀態陣列可以包含任何資料列的 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR。 它會針對它偵測為已更新、刪除或插入的資料列，傳回 SQL_ROW_UPDATED、SQL_ROW_DELETED 或 SQL_ROW_ADDED。  
  
 索引鍵集驅動的資料指標通常是藉由建立包含結果集中每個資料列之索引鍵的臨時表來執行。 因為資料指標也必須判斷資料列是否已更新，所以此資料表通常也包含資料列版本設定資訊的資料行。  
  
 若要在原始結果集上滾動，索引鍵集驅動資料指標會在臨時表上開啟靜態資料指標。 若要抓取原始結果集中的資料列，資料指標會先從臨時表抓取適當的索引鍵，然後取得資料列的目前值。 如果使用區塊資料指標，則資料指標必須取出多個索引鍵和資料列。
