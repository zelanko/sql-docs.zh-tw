---
title: 監視與 System Center Operations Manager (AP) 的應用裝置
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de6cbf6e-f2e9-4877-94df-9c13b1182d56
caps.latest.revision: 14
ms.openlocfilehash: 02bdd22c66729ab471298e211b619e1cb1e4565c
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="monitor-the-appliance-by-using-system-center-operations-manager"></a>使用 System Center Operations Manager 監視的應用裝置
這會說明如何使用 System Center Operations Manager 來監視 SQL Server PDW 和 HDInsight。  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>필수 구성 요소  
  
1.  System Center Operations Manager 2007 R2、 2012年或 2012 SP1 必須安裝且正在執行。  
  
2.  必須安裝 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  監視 SQL Server PDW 和 HDInsight 的管理組件必須安裝、 匯入，並設定。 使用下列指示來執行這些工作。  
  
    -   [安裝 SCOM 管理組件&#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)  
  
    -   [PDW 的 SCOM 管理組件匯入&#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [設定 SCOM 監視 Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>可監視 SQL Server PDW 與 SCOM  
設定 SCOM 管理組件之後, 監視窗格的 SCOM 按一下，然後向下鑽研至**SQL Server 應用裝置**然後**Microsoft SQL Server Parallel Data Warehouse**。 Microsoft SQL Server Parallel Data Warehouse 下方有四個選項： 警示、 裝置、 應用裝置圖表和節點。  
  
### <a name="alerts"></a>警示  
警示是您可以在哪裡找到目前的警示管理。  
  
![Alerts](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>應用裝置  
應用裝置是您可以在其中找到您的環境中目前已探索及監視 SQL Server PDW 應用裝置。 如果應用裝置則不會顯示以下，而且您已建立的 ODBC 連接，然後可能有問題 PDWWatcher 帳戶。 如果它們顯示為 「 未受監視 」 可能有問題 PDWMonitor 帳戶。 請耐心 SCOM 即時，不會變更，但是會定期檢查新的應用裝置，若要監視的並定期將查詢傳送至應用裝置進行監視。  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>應用裝置圖表  
應用裝置圖表頁面是您可以在其中取得查看樹狀結構檢視您的應用裝置的健全狀況：  
  
![應用裝置圖表](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>節點  
最後，節點檢視可讓您查看您的應用裝置，透過每個節點的健全狀況：  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[了解管理主控台警示&#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
