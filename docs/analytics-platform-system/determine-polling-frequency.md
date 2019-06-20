---
title: 判斷輪詢頻率-Analytics Platform System |Microsoft Docs
description: 這篇文章說明如何判斷 Analytics Platform System appliance 警示的輪詢頻率。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: eec9e3e211c68b7f56fe6829a70064317b96e646
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63221990"
---
# <a name="determine-polling-frequency"></a>判斷輪詢頻率
這篇文章說明如何判斷 Analytics Platform System appliance 警示的輪詢頻率。  
  
## <a name="to-determine-the-polling-frequency"></a>若要判斷輪詢頻率  
由於 PDW 目前不支援主動通知警示發生時，監視解決方案，就必須持續輪詢設備 Dll。  就內部而言，PDW 輪詢元件在不同的時間間隔：  
  
-   叢集-60 秒  
  
-   活動訊號-60 秒  
  
-   所有其他元件-5 分鐘  
  
-   效能計數器-三秒  
  
一般間隔輪詢是否有警示，也會使用 System Center，這是**每隔 15 分鐘**。  很明顯地，您可以增加或減少經常查詢，但不是建議使用輪詢小於每 6 小時。  
  
更頻繁地輪詢是可接受的但輪詢太過頻繁可以干擾[sys.dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV。  輪詢太過頻繁變得相當困難的使用者，以診斷查詢效能問題時其快速彙超出檢視。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[設備監視&#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
