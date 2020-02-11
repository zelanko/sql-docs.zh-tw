---
title: 判斷輪詢頻率
description: 本文說明如何判斷分析平臺系統裝置警示的輪詢頻率。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 005fe3d14a7314f7339157064b248a81044a1dfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401208"
---
# <a name="determine-polling-frequency"></a>判斷輪詢頻率
本文說明如何判斷分析平臺系統裝置警示的輪詢頻率。  
  
## <a name="to-determine-the-polling-frequency"></a>判斷輪詢頻率  
由於 PDW 目前不支援警示發生時的主動式通知，因此監視解決方案需要持續輪詢設備 Dll。  就內部而言，PDW 會以不同的間隔輪詢元件：  
  
-   叢集-60 秒  
  
-   心跳-60 秒  
  
-   所有其他元件-五分鐘  
  
-   效能計數器-三秒  
  
輪詢警示的常見間隔時間（也就是 System Center 所使用）是**每15分鐘一次**。  很明顯地，您可以查詢更多或較少，但不建議每隔六小時輪詢一次。  
  
更頻繁的輪詢是可接受的，但是輪詢太頻繁可能會讓[dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV 變得雜亂。  輪詢太頻繁可能會讓使用者難以在其快速地向外流覽時診斷查詢效能問題。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[&#40;分析平臺系統&#41;的設備監視](appliance-monitoring.md)  
  
