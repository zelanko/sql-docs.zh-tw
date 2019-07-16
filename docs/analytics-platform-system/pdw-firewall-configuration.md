---
title: PDW 防火牆設定-Analytics Platform System |Microsoft Docs
description: 防火牆 頁面的 SQL Server PDW 組態管理員可讓您啟用或停用防火牆規則來允許或防止 Analytics Platform System appliance 的特定通訊埠存取。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6f650aac34e3a5299cabae500a8ee73250c3974d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960413"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Analytics Platform System 中的平行資料倉儲防火牆組態

**防火牆**頁面的 SQL Server PDW 組態管理員可讓您啟用或停用防火牆規則來允許或防止 Analytics Platform System appliance 的特定通訊埠存取。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>若要管理連接埠和防火牆應用裝置節點的規則  
  
1.  啟動組態管理員。 如需詳細資訊，請參閱 <<c0> [ 啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。</c0>  
  
2.  在左窗格的 Configuration Manager 中，依序展開**平行資料倉儲拓樸**，然後按一下**防火牆**。  
  
3.  找出的連接埠或防火牆規則來更新組態 清單中，然後選取或清除該項目旁的方塊。 SQL Server PDW 系統管理員可設定選項會顯示在此清單中，包括開啟和關閉連接埠對外節點。  
  
4.  按一下 **套用**以儲存變更。  
  
![DWConfig 應用裝置 PDW 防火牆](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部連接埠  
下列的連接埠已開啟用於來自 PDW 之外的用戶端連線。  
  
|用途|連接埠的 #|節點|  
|-----------|-----------|---------|  
|SQL 用戶端存取 PDW (TDS)|17001|CTL|  
|載入器用戶端存取 （dwloader 和 SSIS）|8001|CTL|  
|遠端桌面存取|3389|CMP 的 CTL|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL 加密連線 （適用於內部通訊，來存取系統管理員主控台）|443|所有節點|  
|SQL Server PDW 負載控制流程 Windows 認證|8002|CTL|  
|Kerberos （_k)|88|AD01 和 ad02 移，|  
|_ldap|389|AD01 和 ad02 移|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>內部連接埠  
下列連接埠 pdw 用於內部通訊，但不是會開啟來自外部 PDW 應用裝置的連線。  
  
|用途|連接埠的 #|節點|  
|-----------|-----------|---------|  
|DMS 控制通道流量|16450|CMP 的 CTL|  
|DMS 資料通道流量|16550|CMP 的 CTL|  
|內部診斷|16650|CMP 的 CTL|  
|容錯移轉狀態 (DMS)|15000|CMP 的 CTL|  
|容錯移轉狀態 (Engine)|15001|CMP|  
|動態 （暫時） 的連接埠範圍|20000-65535|CMP 的 CTL|  
|SQL Server 連接埠範圍 (TDS)|1433, 1500-1508|CMP 的 CTL|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> 建立外部資料表或外部資料來源會使用預設的 TCP 連接埠 8020。 這些陳述式可以設定改為使用其他連接埠。 50300 為 Hortonworks JOB_TRACKER_LOCATION 預設連接埠。 與其他系統和工具整合，可能需要額外的連接埠。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
