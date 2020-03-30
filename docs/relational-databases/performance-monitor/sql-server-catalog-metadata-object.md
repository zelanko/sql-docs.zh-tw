---
title: SQL Server 的 Catalog Metadata 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 3b408951b0a1f32bda0920260aae18ab93350fdd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67986721"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, Catalog Metadata Object
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**SQLServer:Catalog Metadata** 效能物件提供 SQL Server 之目錄中繼資料的計數器。

下表描述 SQL Server **Catalog Metadata** 效能物件。


|**SQL Server Catalog Metadata 計數器**|描述|  
|-------------|-----------------|  
|**Cache Entries Count**|目錄中繼資料快取中的項目數。|
|**Cache Entries Pinned Count**|已釘選的目錄中繼資料快取項目數。|
|**Cache Hit Ratio**|目錄中繼資料快取叫用數與查閱數之間的比率。|
|**Cache Hit Ratio Base**|僅供內部使用。|

每個資料庫都有一個計數器執行個體。

## <a name="see-also"></a>另請參閱  
[監視資源使用狀況 (系統監視器)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
