---
title: 將伺服器設定為在特定 TCP 連接埠上接聽 | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 234996e85d88e9bed0313c2bf3abbf5f81eae65a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port"></a>將伺服器設定為在特定 TCP 連接埠上接聽
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 SQL Server 組態管理員，將 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體設定為在特定固定通訊埠上接聽。 當啟用時，預設的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體會在 TCP 通訊埠 1433 上接聽。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的具名執行個體是針對 [動態通訊埠](https://msdn.microsoft.com/library/dd981060)所設定。 這表示，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動時，它們會選取可用的通訊埠。 透過防火牆連接到具名執行個體時，設定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽特定通訊埠，如此才能在防火牆中開啟適當的通訊埠。  

因為連接埠 1433 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已知標準，所以某些組織會指定應該變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接埠號碼以加強安全性。 這可能有助於某些環境中。 不過，TCP/IP 架構允許[連接埠掃描器](https://wikipedia.org/wiki/Port_scanner)查詢開放的連接埠，因此變更連接埠號碼不是強固安全性量值。

 如需預設 Windows 防火牆設定的詳細資訊以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
> [!TIP]  
>  選取通訊埠編號時，請參閱 [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers)，以取得指派給特定應用程式的通訊埠編號清單。 選取未指派的通訊埠編號。 如需詳細資訊，請參閱 [The default dynamic port range for TCP/IP has changed in Windows Vista and in Windows Server 2008](http://support.microsoft.com/kb/929851)(在 Windows Vista 和 Windows Server 2008 中，TCP/IP 的預設動態通訊埠範圍已變更)。  
  
> [!WARNING]  
>  資料庫引擎會在重新啟動之後開始接聽新的通訊埠。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務會監視登錄，並在組態變更時回報新的通訊埠編號，即使資料庫引擎可能不會用到亦然。 重新啟動資料庫引擎可確保一致性並避免連接失敗。  
  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>若要為 SQL Server Database Engine 指派 TCP/IP 通訊埠編號  
  
1.  在 SQL Server 組態管理員的主控台窗格中，依序展開 [SQL Server 網路組態] 和 [\<執行個體名稱> 的通訊協定]，然後按兩下 [TCP/IP]。  
  
    > [!NOTE]  
    >  如果您無法開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請參閱 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。  
  
2.  在 [TCP/IP 內容] 對話方塊的 [IP 位址] 索引標籤上會出現數個 IP 位址，這些 IP 位址的格式是 **IP1**、**IP2** 到 **IPAll**。 其中一個是供回送介面卡的 IP 位址 127.0.0.1 使用。 同時會出現額外的 IP 位址代表電腦上的每個 IP 位址。 (您可能會看到 IP 第 4 版和 IP 第 6 版位址。)以滑鼠右鍵按一下每個位址，然後按一下 [屬性] 以識別要設定的 IP 位址。  
  
3.  如果 **[TCP 動態通訊埠]** 對話方塊包含 **0**，代表 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在接聽動態通訊埠，請將 0 刪除。  
  
     ![TCP_ports](../../database-engine/configure-windows/media/tcp-ports.png "TCP_ports")  
  
4.  在 [IPn 內容] 區域方塊的 [TCP 通訊埠] 方塊中，鍵入要此 IP 位址接聽的通訊埠編號，然後按一下 [確定]。  
  
5.  在主控台窗格中，按一下 **[SQL Server 服務]**。  
  
6.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server (\<執行個體名稱>)]，然後按一下 [重新啟動]，以停止並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="connecting"></a>Connecting  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽特定通訊埠之後，有三種方式可利用用戶端應用程式連接到特定通訊埠：  
  
-   執行伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務，依名稱連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。  
-   在用戶端上建立別名，指定通訊埠編號。  
-   設定用戶端使用自訂連接字串進行連接。  
  
## <a name="see-also"></a>另請參閱  
 [建立或刪除用戶端使用的伺服器別名 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [SQL Server Browser 服務](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
