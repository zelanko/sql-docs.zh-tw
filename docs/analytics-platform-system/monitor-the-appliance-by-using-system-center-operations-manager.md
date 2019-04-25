---
title: 透過 SCOM-分析平台系統監視 |Microsoft Docs
description: 使用 System Center Operations Manager (SCOM)，以監視 Analytics Platform System (APS) 設備。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3c43734dbd7ef1a766f3f1258f97565ab82e175d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639834"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>監視與 System Center Operations Manager-Analytics Platform System
使用 System Center Operations Manager (SCOM)，以監視 Analytics Platform System (APS) 設備。
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
  
1.  System Center Operations Manager 2007 R2、 2012年或 2012 SP1 必須安裝且正在執行。  
  
2.  必須先安裝 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  若要監視 SQL Server PDW 的管理組件必須安裝、 匯入，並設定。 您可以使用以下文章中的指示來執行這些工作。  
  
    -   [安裝 SCOM 管理組件&#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [匯入適用於 PDW 的 SCOM 管理組件&#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [設定 SCOM 以監視 Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>監視 SQL Server PDW 與 SCOM  
設定 SCOM 管理組件之後, 按一下監視窗格中的 SCOM，然後向下切入至**SQL Server 設備**，然後**Microsoft SQL Server Parallel Data Warehouse**。 Microsoft SQL Server Parallel Data Warehouse，下方有四個選項：警示、 設備，設備圖表和節點。  
  
### <a name="alerts"></a>警示  
警示是您可以在哪裡找到目前的警示管理。  
  
![Alerts](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>應用裝置  
設備是您將在其中找到您的環境中目前已探索和監視 SQL Server PDW 應用裝置。 如果設備未這裡顯示，而且您已建立的 ODBC 連接，則可能會有 PDWWatcher 帳戶發生錯誤。 如果它們會顯示為 「 未受監視 」，可能有 PDWMonitor 帳戶發生錯誤。 因為 SCOM 不會變更，但會定期檢查新的設備，若要監視的耐心等候，定期將查詢傳送到設備的監視。  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>應用裝置圖表  
應用裝置圖表頁面是設備的您可以在其中取得了解您，樹狀結構檢視的健全狀況：  
  
![應用裝置圖表](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>節點  
最後，[節點] 檢視可讓您查看您的應用裝置，透過每個節點的健全狀況：  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解管理主控台警示&#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
