---
title: 判斷輪詢頻率-Analytics Platform System |Microsoft 文件
description: 本文說明如何判斷 Analytics Platform System 應用裝置警示的輪詢頻率。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e8e2a1ccf469e6c587870c0d5921014d797f87d1
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="determine-polling-frequency"></a>判斷輪詢頻率
本文說明如何判斷 Analytics Platform System 應用裝置警示的輪詢頻率。  
  
## <a name="to-determine-the-polling-frequency"></a>若要判斷輪詢頻率  
由於 PDW 目前不支援主動式通知出現警示時，監視解決方案，就必須持續輪詢應用裝置的 Dll。  就內部而言，PDW 輪詢元件在不同的時間間隔：  
  
-   叢集-60 秒  
  
-   活動訊號-60 秒  
  
-   所有其他元件 – 五分鐘  
  
-   效能計數器 – 3 秒  
  
一般警示，輪詢間隔也使用 System Center，這個是**每隔 15 分鐘**。  很明顯地，您可以增加或減少經常查詢，但不是建議使用輪詢小於每隔六小時。  
  
更頻繁地輪詢可接受的但太過頻繁的輪詢可以干擾[sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV。  輪詢頻率太高可能會讓您難以診斷查詢效能的使用者發出時他們快速地復原到檢視。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[應用裝置監視&#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
