---
title: 使用 System Center Operations Manager 來監視 AP
description: 使用 System Center Operations Manager （SCOM）來監視分析平臺系統（AP）應用裝置。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 539c18efe43afcf5436c6913c20cab081974b7f5
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86941120"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>使用 System Center Operations Manager 分析平臺系統進行監視
使用 System Center Operations Manager （SCOM）來監視分析平臺系統（AP）應用裝置。
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
  
1.  System Center Operations Manager 2007 R2、2012或 2012 SP1 必須已安裝且正在執行。  
  
2.  必須安裝 SQL Server 2008 R2 Native Client 或 SQL Server 2012 Native Client。  
  
3.  要監視 SQL Server PDW 的管理元件必須安裝、匯入及設定。 如需執行這些工作的指示，請使用下列文章。  
  
    -   [&#40;Analytics Platform System 安裝 SCOM 管理元件&#41;](install-the-scom-management-packs.md)  
  
    -   [匯入適用于 PDW 的 SCOM 管理元件 &#40;分析平臺系統&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [設定 SCOM 以監視分析平臺系統 &#40;分析平臺系統&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>使用 SCOM 監視 SQL Server PDW  
設定 SCOM 管理元件之後，請按一下 SCOM 的 [監視中] 窗格，向下切入至**SQL Server 設備**，然後**Microsoft SQL Server 平行處理資料倉儲**]。 在 Microsoft SQL Server 平行處理資料倉儲底下，有四個選擇： [警示]、[設備]、[設備] 圖表和 [節點]。  
  
### <a name="alerts"></a>警示  
警示是您可以在其中找到要管理之目前警示的位置。  
  
![警示](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>應用裝置  
設備可讓您在環境中找到目前已探索和受監視的 SQL Server PDW 設備。 如果設備未顯示在這裡，而您已為其建立 ODBC 連線，則您的 PDWWatcher 帳戶可能發生問題。 如果它們顯示為「未受監視」，您的 PDWMonitor 帳戶可能發生問題。 請耐心等候，因為 SCOM 不會即時進行變更，但會定期檢查是否有新的設備進行監視，並定期將查詢傳送至設備以進行監視。  
  
![用具](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>設備圖  
[設備關係圖] 頁面可讓您查看設備的健康情況，其中包含樹狀檢視：  
  
![應用裝置圖表](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>節點  
最後，[節點] 視圖可讓您透過每個節點查看設備的健全狀況：  
  
![節點](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[瞭解管理主控台警示 &#40;分析平臺系統&#41;](understanding-admin-console-alerts.md)  
  
