---
title: PolyBase 向外延展群組 | Microsoft Docs
description: 使用 PolyBase 群組功能來建立 SQL Server 執行個體的叢集。 這可以改善來自外部來源的大型資料集查詢效能。
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sql13.swb.polybasescaleoutcluster.page.f1
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 3928d00a2b72c4d1484fa8b30ca579a5af0ef34c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416339"
---
# <a name="polybase-scale-out-groups"></a>PolyBase 向外延展群組

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

含有 PolyBase 的獨立 SQL Server 執行個體會在處理 Hadoop 或 Azure Blob 儲存體中的大量資料集時成為效能瓶頸。 PolyBase 群組功能可讓您建立 SQL Server 執行個體的叢集，利用向外延展方式處理來自外部資料來源 (例如 Hadoop 或 Azure Blob 儲存體) 的大型資料集，以提高查詢效能。 您現在可以調整 SQL Server 計算，以符合您工作負載的效能需求。 PolyBase 向外延展群組是一組 SQL Server 執行個體，能讓您在平行處理結構中處理龐大的外部資料集。 當您將更多 SQL Server 執行個體新增至群組時，資料載入及查詢效能可線性增加。 
  
請參閱 [開始使用 PolyBase](./polybase-guide.md) 和 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)。
  
![顯示 PolyBase 向外延展群組的圖表。](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase 向外延展群組")  
  
## <a name="head-node"></a>前端節點  

前端節點包含要提交 PolyBase 查詢的目標 SQL Server 執行個體。 每個 PolyBase 群組只能包含一個前端節點。 前端節點是 SQL Server 執行個體上 SQL Server 資料庫引擎、PolyBase 引擎與 PolyBase 資料移動服務的邏輯群組。 使用 SQL Server 2017 與 SQL Server 2016 時，前端節點必須是 Enterprise 版本。 從 SQL Server 2019 開始，PolyBase 前端節點可以是 Enterprise 或 Standard 版本。
  
## <a name="compute-node"></a>計算節點

計算節點包含 SQL Server 執行個體，可協助處理外部資料上的向外延展查詢。 計算節點是 SQL Server 執行個體上 SQL Server 和 PolyBase Data Movement Service 的邏輯群組。 一個 PolyBase 群組可以有多個計算節點。 前端節點和計算節點全都必須執行同一個 SQL Server 版本。 SQL Server 2016 的初始版本允許計算節點為 Enterprise 或 Standard 版本。 從 SQL Server 2016 SP1 開始，所有版本的 SQL Server 都可以成為計算節點。

## <a name="scale-out-reads"></a>向外延展讀取

當查詢外部 SQL Server、Oracle 或 Teradata 執行個體時，資料分割資料表會因向外延展讀取而獲益。 PolyBase 向外延展群組中的每個節點最多可啟動 8 個讀取器來讀取外部資料。 而且每個讀取器會獲派一個要在外部資料表中讀取的分割區。 

例如，假設您有個外部 SQL Server 資料表，其具有 12 個月的分割區，以及有 3 個節點的 PolyBase 向外延展群組，則每個節點各會使用 4 個 PolyBase 讀取器來處理這 12 個分割區。 如下圖所示。 

> [!NOTE]
>  這與透過 Hadoop 進行的向外延展讀取不同。 

![PolyBase 向外延展讀取](../../relational-databases/polybase/media/polybase-scale-out-groups2.png "PolyBase 向外延展群組")
  
## <a name="distributed-query-processing"></a>分散式查詢處理  

PolyBase 查詢會提交到前端節點上的 SQL Server。 參考外部資料表之查詢的這一部分會交付至 PolyBase Engine。
  
PolyBase Engine 是 PolyBase 查詢背後的重要元件。 它會剖析外部資料的查詢、產生查詢計劃，以及將工作分散到計算節點上的資料移動服務加以執行。 工作完成之後，它會接收來自計算節點的結果，然後提交給 SQL Server 進行處理並傳回給用戶端。
  
PolyBase Data Movement Service 會接收來自 PolyBase Engine 的指示，並在 HDFS 與 SQL Server 之間傳輸資料，以及在前端和計算節點上的 SQL Server 執行個體之間傳輸資料。
  
## <a name="next-steps"></a>後續步驟

若要設定 PolyBase 向外延展群組，請參閱下列指南：

[Improve PolyBase scale-out groups on Windows](configure-scale-out-groups-windows.md) (在 Windows 上改進 PolyBase 向外延展群組)

## <a name="see-also"></a>另請參閱

 [sys-dm-exec-compute-nodes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)   
 [sys-dm-exec-compute-node-status](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)   
 [sys.dm_exec_compute_node_errors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)
