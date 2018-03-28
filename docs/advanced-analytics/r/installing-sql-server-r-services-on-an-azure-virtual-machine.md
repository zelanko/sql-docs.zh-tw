---
title: 在 Azure 虛擬機器上安裝 SQL Server 的機器學習功能 |Microsoft 文件
ms.custom: ''
ms.date: 03/21/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: ''
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: d2f0f38086c7725e14261afa9a40f29b212b748f
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="install-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>安裝 SQL Server 機器學習在 Azure 虛擬機器上的功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
我們建議您使用[資料 Science 虛擬機器](ttps://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm)，但如果您想 VM 時，只有 SQL Server 2017 機器學習服務或 SQL Server 2016 R 服務，這篇文章會引導您逐步完成。

## <a name="create-a-virtual-machine-on-azure"></a>在 Azure 上建立虛擬機器

1. 在 Azure 入口網站左側的清單中，按一下**虛擬機器**，然後按一下 **新增**。
2. 搜尋 SQL Server 2017 Enterprise Edition 或 SQL Server 2016 Enterprise Edition。
3. 設定伺服器名稱和帳戶權限，並選取一個定價方案。
4. 在**SQL Server 設定**(步驟 4 中 VM 安裝精靈中)，找出**機器學習服務 (Advanced Analytics)** (或**R Services**適用於 SQL Server 2016)，按一下  **啟用**。
5. 檢閱顯示的摘要進行驗證，並按一下 [確定]。
6. 當虛擬機器準備就緒時，連線至虛擬機器並開啟預先安裝的 SQL Server Management Studio。 機器學習服務已準備好執行。
7. 若要驗證這一點，您可以開啟新的查詢視窗，並執行簡單的陳述式，如下所示，它使用 R 來產生從 1 到 10 的數字序列。

    ```
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
    ```

6. 如果您打算從遠端資料科學用戶端連接的執行個體時，完成[額外的步驟](#additional-steps)視。

### <a name="disable-machine-learning-features-on-a-sql-server-vm"></a>停用 SQL Server VM 上的機器學習功能

您也可以啟用或停用現有的 SQL Server 虛擬機器上的功能，在任何時間。

1. 開啟虛擬機器刀鋒視窗。
2. 按一下 [設定]，並選取 [SQL Server 組態]。
3. 對功能進行變更，並套用。

### <a name="existing"></a>將 R 服務新增到現有的 SQL Server 2016 Enterprise VM

如果您建立 Azure 機器學習服務不包含 SQL Server 虛擬機器，您可以加入功能，依照下列步驟：

1. 重新執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式，並在精靈的 [伺服器組態] 頁面上新增該功能。
2. 啟用外部指令碼執行，並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱[安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。
3. (選擇性) 如果遠端指令碼執行需要，請設定 R 背景工作帳戶的資料庫存取權。
4. (選擇性) 如果您想要允許從遠端資料科學用戶端執行 R 指令碼，請修改 Azure 虛擬機器上的防火牆規則。 如需詳細資訊，請參閱[解除封鎖防火牆](#firewall)。
5. 安裝或啟用必要的網路程式庫。 如需詳細資訊，請參閱[新增網路通訊協定](#network)。

## <a name="additional-steps"></a>額外的步驟

如果預期遠端用戶端存取與遠端的 SQL Server 計算內容伺服器需要一些額外的步驟。

### <a name="firewall"></a>解除封鎖防火牆

根據預設，Azure 虛擬機器上的防火牆會包含會封鎖網路本機使用者帳戶的存取權的規則。

您必須停用此規則，確保您可以存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從遠端資料科學用戶端的執行個體。  否則，您的機器學習程式碼無法使用虛擬機器的工作區的計算內容中執行。

若要啟用從遠端資料科學用戶端存取：

1. 在虛擬機器上，開啟 [具有進階安全性的 Windows 防火牆]。
2. 選取 [輸出規則]
3. 停用下列規則︰
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>針對遠端用戶端啟用 ODBC 回呼

如果您預期呼叫伺服器的用戶端必須發出 ODBC 查詢做為其機器學習解決方案的一部分，您必須確定 [啟動列] 可讓伺服器代表遠端用戶端的 ODBC 呼叫。 若要這樣做，您必須允許 Launchpad 所使用的 SQL 背景工作帳戶登入執行個體。
如需詳細資訊，請參閱[安裝 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)。

### <a name="network"></a>新增網路通訊協定

+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會針對用戶端和伺服器電腦之間的連線，以及部分內部連線使用「具名管道」通訊協定。 如果未啟用具名管道，您必須同時在 Azure 虛擬機器以及連線 到伺服器的任何資料科學用戶端上，安裝具名管道並將它啟用。
  
+ 啟用 TCP/IP

  TCP/IP 是回送連接的必要項。 如果您收到下列錯誤，請在支援的執行個體的虛擬機器上啟用 TCP/IP:

  「 DBNETLIB;SQL Server 不存在或拒絕存取 」