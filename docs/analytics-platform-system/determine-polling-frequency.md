---
title: "判斷輪詢頻率 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: "7"
ms.openlocfilehash: fb32abc38a90cd7450dc310a9f73eb7a5d72b5fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="determine-polling-frequency"></a>判斷輪詢頻率
本主題說明如何判斷 SQL Server PDW 應用裝置警示的輪詢頻率。  
  
## <a name="to-determine-the-polling-frequency"></a>若要判斷輪詢頻率  
由於 PDW 目前不支援主動式通知出現警示時，監視解決方案，就必須持續輪詢應用裝置的 Dll。  就內部而言，PDW 輪詢元件在不同的時間間隔：  
  
-   叢集-60 秒  
  
-   活動訊號-60 秒  
  
-   所有其他元件-5 分鐘  
  
-   效能計數器 – 3 秒  
  
一般警示，輪詢間隔也使用 System Center，這個是**每隔 15 分鐘**。  很明顯地，您可以增加或減少經常查詢，但不是建議使用輪詢小於每 6 小時。  
  
更頻繁地輪詢可接受的但太過頻繁的輪詢可以干擾[sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV。  這可讓使用者診斷查詢效能問題很難那里查詢快速復原超出檢視。  
  
## <a name="see-also"></a>請參閱＜  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[應用裝置監視 &#40;Analytics Platform System &#41;](appliance-monitoring.md)  
  
