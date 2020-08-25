---
title: 判斷輪詢頻率
description: 本文說明如何判斷 Analytics Platform System 設備警示的輪詢頻率。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafd18a7701ed5de5018a3e8dc23bc8d5d9640fa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767037"
---
# <a name="determine-polling-frequency"></a>判斷輪詢頻率
本文說明如何判斷 Analytics Platform System 設備警示的輪詢頻率。  
  
## <a name="to-determine-the-polling-frequency"></a>判斷輪詢頻率  
由於 PDW 目前不支援警示發生時的主動式通知，監視解決方案需要持續輪詢設備 Dll。  在內部，PDW 會以不同的間隔輪詢元件：  
  
-   叢集-60 秒  
  
-   信號-60 秒  
  
-   所有其他元件-五分鐘  
  
-   效能計數器-三秒  
  
輪詢警示的常見間隔（System Center 也會使用此間隔）是 **每隔15分鐘**。  很明顯地，您可以更頻繁地查詢，但不建議您輪詢不到每6小時。  
  
更頻繁地進行輪詢是可接受的，但是輪詢太頻繁可能會造成 [sys. dm_pdw_nodes_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md?view=sql-server-ver15) DMV 混亂。  太頻繁地輪詢可能會讓使用者在快速推出查詢效能問題時，難以診斷。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[設備監視 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
