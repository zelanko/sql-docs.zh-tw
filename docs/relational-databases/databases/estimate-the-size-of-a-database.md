---
title: 估計資料庫的大小 | Microsoft Docs
description: 當在 SQL Server 中設計資料庫時，評估其大小可協助判斷效能與磁碟空間所需的硬體設定。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0645fdf69d5d1cc2859388c20e6170e3a152c0d9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474129"
---
# <a name="estimate-the-size-of-a-database"></a>估計資料庫的大小
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  在設計資料庫時，您可能需要估計資料庫填滿資料時的大小。 估計資料庫的大小可協助您判斷執行下列事項所需的硬體組態：  
  
-   達到應用程式所需的效能。  
  
-   提供需要的適當磁碟空間實際數量來儲存資料和索引。  
  
 估計資料庫的大小也可幫助您判斷是否需要調整資料庫設計。 例如您可判斷估計的資料庫大小是否太大，而導致無法實作於公司之中，並需要進一步地正規化。 相反的，估計的大小可能小於預期的大小。 這樣可讓您取消正規化資料庫進而提升查詢效能。  
  
 若要估計資料庫的大小，可先個別地估計每個資料表的大小，然後將得到的數值加總。 資料表的大小取決於資料表是否包含索引，若包含索引，則必須判斷索引的類型為何。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[估計資料表的大小](../../relational-databases/databases/estimate-the-size-of-a-table.md)|定義必要的步驟和計算，來估計將資料儲存於資料表和相關聯索引所需的空間數量。|  
|[估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|定義必要的步驟和計算，來估計將資料儲存於堆積所需的空間數量。 堆積是沒有叢集索引的資料表。|  
|[估計叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|定義必要的步驟和計算，來估計將資料儲存於叢集索引所需的空間數量。|  
|[估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|定義必要的步驟和計算，來估計將資料儲存於非叢集索引所需的空間數量。|  
  
  
