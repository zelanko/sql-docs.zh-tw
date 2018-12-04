---
title: SQL Server 的 Catalog Metadata 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0474646ae51a8fdabe6ff139c6eff1ec966f8d93
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158806"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, Catalog Metadata Object
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**SQLServer:Catalog Metadata** 效能物件提供 SQL Server 之目錄中繼資料的計數器。

下表描述 SQL Server **Catalog Metadata** 效能物件。


|**SQL Server Catalog Metadata 計數器**|Description|  
|-------------|-----------------|  
|**Cache Entries Count**|目錄中繼資料快取中的項目數。|
|**Cache Entries Pinned Count**|已釘選的目錄中繼資料快取項目數。|
|**Cache Hit Ratio**|目錄中繼資料快取叫用數與查閱數之間的比率。|
|**Cache Hit Ratio Base**|僅供內部使用。|

每個資料庫都有一個計數器執行個體。

## <a name="see-also"></a>另請參閱  
[監視資源使用狀況 (系統監視器)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
