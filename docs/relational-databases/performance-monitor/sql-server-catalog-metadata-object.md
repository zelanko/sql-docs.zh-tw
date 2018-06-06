---
title: SQL Server 的 Catalog Metadata 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
caps.latest.revision: 4
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: 484dc0c7be3b7ca67c3645e6b8f088839d4bf631
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
