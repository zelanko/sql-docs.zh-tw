---
title: "在 Azure 虛擬機器上安裝 SQL Server 的機器學習功能 |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0f1e597d4b6ddda30938108badc0bf31b0108bc4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="installing-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>安裝 SQL Server 機器學習在 Azure 虛擬機器上的功能
 
如果您部署 Azure 虛擬機器包含[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，您現在可以選取機器學習為 VM 建立時，要加入至執行個體功能。

+ [建立新的 VM 包含 SQL Server 2016 和 R 服務](#new)
+ [機器學習功能加入現有 SQL Server 2016 的虛擬機器](#existing)

> [!NOTE]
> 虛擬機器現在可供 SQL Server 2017 ！ 請參閱[這項公告](https://azure.microsoft.com/blog/announcing-new-azure-vm-images-sql-server-2017-on-linux-and-windows/)如需詳細資訊。
> 
> R 也可做為 Azure SQL Database 中的預覽功能。 如需詳細資訊，請參閱[使用 Azure SQL Database 中的 R](../r/using-r-in-azure-sql-database.md)。

## <a name="create-a-new-sql-server-2017-virtual-machine"></a>建立新的 SQL Server 2017 虛擬機器

若要在 SQL Server 2017 中使用 R 或 Python，務必要取得 Windows 型虛擬機器。 [!INCLUDE[sscurrentlong-md](../../includes/sscurrentlong-md.md)]在 Linux 上支援快速[原生計分](../sql-native-scoring.md)使用 T-SQL 預測函式，但其他機器學習功能未提供尚未在這個版本中。

SQL Server VM 的供應項目的清單，請參閱這篇文章：[概觀的 SQL Server 在 Azure 虛擬機器 (Windows)](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)。

### <a name="new"></a>建立具有機器學習新的 SQL Server Enterprise VM

1. 在 Azure 入口網站中，按一下虛擬機器，然後按一下 [新增]。
2. 選取 SQL Server 2017 Enterprise Edition。
3. 設定伺服器名稱和帳戶權限，並選取一個定價方案。
4. 在**SQL Server 設定**(步驟 4 中 VM 安裝精靈中)，找出**機器學習服務 (Advanced Analytics)**按一下**啟用**。
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
2. 啟用外部指令碼執行，並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱[設定 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. (選擇性) 如果遠端指令碼執行需要，請設定 R 背景工作帳戶的資料庫存取權。
   如需詳細資訊，請參閱[安裝 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. (選擇性) 如果您想要允許從遠端資料科學用戶端執行 R 指令碼，請修改 Azure 虛擬機器上的防火牆規則。 如需詳細資訊，請參閱[解除封鎖防火牆](#firewall)。
4. 安裝或啟用必要的網路程式庫。 如需詳細資訊，請參閱[新增網路通訊協定](#network)。

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
如需詳細資訊，請參閱 [安裝 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。

### <a name="network"></a>新增網路通訊協定

+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會針對用戶端和伺服器電腦之間的連線，以及部分內部連線使用「具名管道」通訊協定。 如果未啟用具名管道，您必須同時在 Azure 虛擬機器以及連線 到伺服器的任何資料科學用戶端上，安裝具名管道並將它啟用。
  
+ 啟用 TCP/IP

  TCP/IP 是回送連接的必要項。 如果您收到下列錯誤，請在支援的執行個體的虛擬機器上啟用 TCP/IP:

  「 DBNETLIB;SQL Server 不存在或拒絕存取 」

## <a name="related-resources"></a>相關資源

[在 Azure SQL Database 中使用 R](../r/using-r-in-azure-sql-database.md)