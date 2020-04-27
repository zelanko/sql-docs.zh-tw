---
title: 建立圖表、警示、記錄和報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f36f1a3df7eae3fd363aa5e2bc4b5ae13f36ae2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63032402"
---
# <a name="create-charts-alerts-logs-and-reports"></a>建立圖表、警示、記錄和報表
  「系統監視器」可讓您建立圖表、警示、記錄和報表，以監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
## <a name="charts"></a>圖表  
 圖表可以監視所選取物件和計數器目前的效能；例如 CPU 使用量或磁碟 I/O。 您可以在圖表中加入各種不同的系統監視器物件和計數器組合。 也可將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 物件和計數器加入圖表。  
  
 每個圖表都代表欲監視之資訊的子集合。 例如一個圖表可追蹤記憶體使用狀況統計資料，第二個圖表可追蹤磁碟 I/O 統計資料。  
  
 使用圖表有助於下列工作：  
  
-   研究為何某個電腦或應用程式很慢或沒有效率。  
  
-   持續監視系統來找出間歇性的效能問題。  
  
-   找出為何需要增加容量的原因。  
  
-   將趨勢顯示成線條圖。  
  
-   將比較資料顯示成分佈圖表。  
  
 圖表對於短期、即時地監視本地或遠端的電腦很有用，例如若要監視事件發生時的狀況。  
  
## <a name="alerts"></a>警示  
 使用警示，可讓「系統監視器」追蹤特定事件，並依要求在發生事件時進行通知。 警示記錄檔可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，監視所選取計數器和物件執行個體的目前效能。 如果計數器超出給定值，記錄檔便會記錄事件的日期和時間。 事件也可以產生網路警示。 您可以在事件第一次發生或每次發生時，指定要執行的程式。 例如，警示可以傳送網路訊息給所有系統管理員，告知 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的磁碟空間不足。  
  
## <a name="logs"></a>記錄  
 記錄檔可讓您記錄選定物件和電腦的目前活動資訊，以供日後檢視與分析。 您可將多個系統的資料收集到一個記錄檔內。 例如，您可以建立不同的記錄檔來累積各種電腦上選取物件的效能資訊，以供日後分析。 您可將這些選取資料存到一個檔名底下，當您想要建立相似資訊的另一個記錄檔以進行比較時，就可重複使用它們。  
  
 記錄檔提供許多資訊，可用於疑難排解或規劃上。 目前活動的圖表、警示與報表可提供立即的回應，而記錄檔則可讓您長期追蹤計數器。 因此，您可以更詳盡地檢查資訊，並記錄系統的效能。  
  
## <a name="reports"></a>報表  
 報表可讓您顯示經常變動的計數器值以及所選取物件的執行個體值。 這些值出現在每個執行個體的資料行中。 您可以調整報表的間隔，列印快照集，以及匯出資料。 當您需要顯示原始數字時，請使用報表。  
  
 如需建立圖表、警示、記錄檔和報表的詳細資訊，以及 Windows 物件和計數器的詳細資訊，請參閱 Windows 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
