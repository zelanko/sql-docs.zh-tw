---
title: "設定用於資料庫引擎存取的 Windows 防火牆 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], firewall systems
- firewall systems, [Database Engine]
- security [SQL Server], firewalls
ms.assetid: 0093b43c-c6b5-4574-9b30-3a0e91e1a1f9
caps.latest.revision: "57"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 93ffea433f68d8b380f6d0d24865e8a6c00429ad
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configure-a-windows-firewall-for-database-engine-access"></a>設定用於 Database Engine 存取的 Windows 防火牆

 > 如需舊版 SQL Server 的相關內容，請參閱[設定 Windows 防火牆以允許資料庫引擎存取](https://msdn.microsoft.com/en-US/library/ms175043(SQL.120).aspx)。


  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定用於 Database Engine 存取的 Windows 防火牆。 防火牆系統有助於預防未經授權存取電腦資源。 若要透過防火牆存取 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦上的防火牆設定為允許存取。  
  
 如需預設 Windows 防火牆設定的詳細資訊以及影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。 有許多防火牆系統可用。 如需系統專用的資訊，請參閱防火牆文件集。  
  
 允許存取的主要步驟包括：  
  
1.  將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用特定 TCP/IP 通訊埠。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的預設執行個體會使用 1433 通訊埠，不過這是可以變更的。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的通訊埠列在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]、[!INCLUDE[ssEW](../../includes/ssew-md.md)] 的執行個體及 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的具名執行個體都使用動態通訊埠。 若要將這些執行個體都設定為使用特定通訊埠，請參閱[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
2.  針對經過授權的使用者或電腦，將防火牆設定為允許存取該通訊埠。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務可讓使用者連接至並未接聽通訊埠 1433 的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，而不用知道通訊埠編號。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser，您必須開啟 UDP 通訊埠 1434。 若要提升至最安全的環境，請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務保留在停止狀態，並將用戶端設定為使用此通訊埠編號連接。  
  
> [!NOTE]  
>  根據預設， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 會啟用 Windows 防火牆，它會關閉通訊埠 1433 來防止網際網路電腦連接到您電腦上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。 除非您重新開啟通訊埠 1433，否則無法使用 TCP/IP 連接至預設執行個體。 下列程序將說明設定 Windows 防火牆的基本步驟。 如需詳細資訊，請參閱 Windows 文件集。  
  
 除了將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接聽固定通訊埠並開啟此通訊埠以外，您也可以列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可執行檔 (Sqlservr.exe) 做為被封鎖程式的例外。 當您想要繼續使用動態通訊埠時，請使用此方法。 不過，這個方法只能存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其中一個執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目，設定用於 Database Engine 存取的 Windows 防火牆：**  
  
     [SQL Server 組態管理員](#SSMSProcedure)  
  
## <a name="before-you-begin"></a>開始之前  
  
###  <a name="Security"></a> 安全性  
 在防火牆中開啟通訊埠可能會讓您的伺服器面臨惡意攻擊的威脅。 請先確定您已了解防火牆系統，然後再開啟通訊埠。 如需相關資訊，請參閱 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
 適用於 Windows Vista、Windows 7 和 Windows Server 2008  
  
 下列程序使用「具有進階安全性的 Windows 防火牆」Microsoft Management Console (MMC) 嵌入式管理單元設定 Windows 防火牆。 「具有進階安全性的 Windows 防火牆」只會設定目前的設定檔。 如需 [具有進階安全性的 Windows 防火牆] 的詳細資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access"></a>若要在 Windows 防火牆中開啟通訊埠以便 TCP 存取  
  
1.  在 **[開始]** 功能表上、按一下 **[執行]**，輸入 **WF.msc**，然後按一下 **[確定]**。  
  
2.  在 **[具有進階安全性的 Windows 防火牆]**的左窗格中，以滑鼠右鍵按一下 **[輸入規則]**，然後按一下動作窗格中的 **[新增規則]** 。  
  
3.  在 **[規則類型]** 對話方塊中，選取 **[通訊埠]**，然後按 **[下一步]**。  
  
4.  在 **[通訊協定及連接埠]** 對話方塊中，選取 **[TCP]**。 選取 **[特定本機連接埠]**，然後輸入 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的通訊埠編號，例如 **1433** 表示預設執行個體。 按 [下一步] 。  
  
5.  在 **[執行動作]** 對話方塊中，選取 **[允許連線]**，然後按 **[下一步]**。  
  
6.  在 **[設定檔]** 對話方塊中，選取您想要連線至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，描述電腦連線環境的設定檔，然後按 **[下一步]**。  
  
7.  在 **[名稱]** 對話方塊中，輸入此規則的名稱和描述，然後按一下 **[完成]**。  
  
#### <a name="to-open-access-to-sql-server-when-using-dynamic-ports"></a>若要在使用動態通訊埠時開放 SQL Server 的存取  
  
1.  在 **[開始]** 功能表上、按一下 **[執行]**，輸入 **WF.msc**，然後按一下 **[確定]**。  
  
2.  在 **[具有進階安全性的 Windows 防火牆]**的左窗格中，以滑鼠右鍵按一下 **[輸入規則]**，然後按一下動作窗格中的 **[新增規則]** 。  
  
3.  在 **[規則類型]** 對話方塊中，選取 **[程式]**，然後按 **[下一步]**。  
  
4.  在 **[程式]** 對話方塊中，選取 **[這個程式路徑]**。 按一下 **[瀏覽]**，並導覽至您想要透過防火牆存取的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，然後按一下 **[開啟]**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設位於 **C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe**。 按一下 **[下一步]**。  
  
5.  在 **[執行動作]** 對話方塊中，選取 **[允許連線]**，然後按 **[下一步]**。  
  
6.  在 **[設定檔]** 對話方塊中，選取您想要連線至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，描述電腦連線環境的設定檔，然後按 **[下一步]**。  
  
7.  在 **[名稱]** 對話方塊中，輸入此規則的名稱和描述，然後按一下 **[完成]**。  
  
## <a name="see-also"></a>另請參閱  
 [如何：設定防火牆設定 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
