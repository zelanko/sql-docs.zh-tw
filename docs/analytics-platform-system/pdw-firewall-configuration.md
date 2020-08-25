---
title: PDW 防火牆設定
description: SQL Server PDW Configuration Manager 的 [防火牆] 頁面可讓您啟用或停用防火牆規則，以允許或防止存取 Analytics Platform System 設備上的特定埠。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400880"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>分析平臺系統中的平行資料倉儲防火牆設定

SQL Server PDW Configuration Manager 的 [ **防火牆** ] 頁面可讓您啟用或停用防火牆規則，以允許或防止存取 Analytics Platform System 設備上的特定埠。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>管理設備節點的埠和防火牆規則  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱 [啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在 Configuration Manager 的左窗格中，展開 [ **平行處理資料倉儲拓撲**]，然後按一下 [ **防火牆**]。  
  
3.  在 [設定] 清單中找出要更新的埠或防火牆規則，然後選取或清除該專案旁的方塊。 此清單中只會顯示 SQL Server PDW 管理員可設定的選項，包括對外節點的開啟和關閉埠。  
  
4.  按一下 [套用] 以儲存 **您的變更** 。  
  
![DWConfig 應用裝置 PDW 防火牆](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部埠  
系統會針對來自 PDW 外部的用戶端連接開啟下列埠。  
  
|目的|港口#|節點|  
|-----------|-----------|---------|  
|適用于 PDW 的 SQL 用戶端存取 (TDS) |17001|Ctl|  
|載入器用戶端存取 (dwloader & SSIS) |8001|Ctl|  
|遠端桌面存取|3389|CTL、CMP|  
|SSIS BinaryLoaderDataChannel|16551|Ctl|  
|dwloader BinaryLoaderDataChannel|16551|Cmp|  
|SSL 加密連線 (進行內部通訊，以存取管理主控台) |443|所有節點|  
|SQL Server PDW 載入控制流程-Windows 認證|8002|Ctl|  
|_Kerberos|88|AD01 和 AD02，|  
|_ldap|389|AD01 和 AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>內部埠  
PDW 會使用下列埠進行內部通訊，但不會針對來自 PDW 設備外的連接開啟。  
  
|目的|港口#|節點|  
|-----------|-----------|---------|  
|DMS 控制通道流量|16450|CTL、CMP|  
|DMS 資料通道流量|16550|CTL、CMP|  
|內部診斷|16650|CTL、CMP|  
| (DMS) 的容錯移轉狀態|15000|CTL、CMP|  
|容錯移轉狀態 (引擎) |15001|Cmp|  
|動態 (暫時) 埠範圍|20000-65535|CTL、CMP|  
|SQL Server (TDS 的埠範圍) |1433、1500-1508|CTL、CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> 建立外部資料表或外部資料源預設會使用 TCP 埠8020。 這些語句可以設定為改用其他埠。 Hortonworks JOB_TRACKER_LOCATION 預設埠是50300。 與其他系統和工具整合可能需要額外的埠。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
