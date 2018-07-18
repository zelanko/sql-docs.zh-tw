---
title: 估計資料庫的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3364f033791dfb0a9798a9f8bf5a311c5af88f7a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221488"
---
# <a name="estimate-the-size-of-a-database"></a>估計資料庫的大小
  在設計資料庫時，您可能需要估計資料庫填滿資料時的大小。 估計資料庫的大小可協助您判斷執行下列事項所需的硬體組態：  
  
-   達到應用程式所需的效能。  
  
-   提供需要的適當磁碟空間實際數量來儲存資料和索引。  
  
 估計資料庫的大小也可幫助您判斷是否需要調整資料庫設計。 例如您可判斷估計的資料庫大小是否太大，而導致無法實作於公司之中，並需要進一步地正規化。 相反的，估計的大小可能小於預期的大小。 這樣可讓您取消正規化資料庫進而提升查詢效能。  
  
 若要估計資料庫的大小，可先個別地估計每個資料表的大小，然後將得到的數值加總。 資料表的大小取決於資料表是否包含索引，若包含索引，則必須判斷索引的類型為何。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[估計資料表的大小](estimate-the-size-of-a-table.md)|定義必要的步驟和計算，來估計將資料儲存於資料表和相關聯索引所需的空間數量。|  
|[估計堆積的大小](estimate-the-size-of-a-heap.md)|定義必要的步驟和計算，來估計將資料儲存於堆積所需的空間數量。 堆積是沒有叢集索引的資料表。|  
|[估計叢集索引的大小](estimate-the-size-of-a-clustered-index.md)|定義必要的步驟和計算，來估計將資料儲存於叢集索引所需的空間數量。|  
|[估計非叢集索引的大小](estimate-the-size-of-a-nonclustered-index.md)|定義必要的步驟和計算，來估計將資料儲存於非叢集索引所需的空間數量。|  
  
  
