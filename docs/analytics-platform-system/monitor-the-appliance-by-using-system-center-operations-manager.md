---
title: 監視器與 SCOM-Analytics Platform System |Microsoft 文件
description: 您可以使用 System Center Operations Manager (SCOM) 來監視 Analytics Platform System (APS) 的應用裝置。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2b26462ab37cf7d63960ff7db6e20c57e8290bb
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>監視與 System Center Operations Manager Analytics Platform System
您可以使用 System Center Operations Manager (SCOM) 來監視 Analytics Platform System (APS) 的應用裝置。
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>필수 구성 요소  
  
1.  System Center Operations Manager 2007 R2、 2012年或 2012 SP1 必須安裝且正在執行。  
  
2.  必須安裝 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  監視 SQL Server PDW 和 HDInsight 的管理組件必須安裝、 匯入，並設定。 您可以使用以下文章中的指示來執行這些工作。  
  
    -   [安裝 SCOM 管理組件&#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [PDW 的 SCOM 管理組件匯入&#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [設定 SCOM 監視 Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>可監視 SQL Server PDW 與 SCOM  
設定 SCOM 管理組件之後, 監視窗格的 SCOM 按一下，然後向下鑽研至**SQL Server 應用裝置**然後**Microsoft SQL Server Parallel Data Warehouse**。 Microsoft SQL Server Parallel Data Warehouse 下方有四個選項： 警示、 裝置、 應用裝置圖表和節點。  
  
### <a name="alerts"></a>警示  
警示是您可以在哪裡找到目前的警示管理。  
  
![警示](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>應用裝置  
應用裝置是您可以在其中找到您的環境中目前已探索及監視 SQL Server PDW 應用裝置。 如果應用裝置則不會顯示以下，而且您已建立的 ODBC 連接，然後可能有問題 PDWWatcher 帳戶。 如果它們顯示為 「 未受監視 」，可能有問題 PDWMonitor 帳戶。 因為 SCOM 即時，不會變更，但也會定期檢查新的應用裝置，若要監視的耐心等候，定期將查詢傳送至應用裝置進行監視。  
  
![應用裝置](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>應用裝置圖表  
應用裝置圖表頁面是您可以在其中取得查看樹狀結構檢視您的應用裝置的健全狀況：  
  
![應用裝置圖表](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>節點  
最後，節點檢視可讓您查看您的應用裝置，透過每個節點的健全狀況：  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解管理主控台警示&#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
