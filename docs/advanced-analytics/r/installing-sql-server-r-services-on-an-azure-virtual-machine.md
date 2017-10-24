---
title: "在 Azure 虛擬機器上安裝 SQL Server R Services | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e673268b1f6b56890f22576d293135b2675ed4ab
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="installing-sql-server-r-services-on-an-azure-virtual-machine"></a>在 Azure 虛擬機器上安裝 SQL Server R Services
 
如果您部署 Azure 虛擬機器包含[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，您現在可以選取機器學習為 VM 建立時，要加入至執行個體功能。

+ [建立具有 SQL Server 2016 和 R Services 的新 VM](#new)
+ [將 R Services 新增至具有 SQL Server 2016 的現有虛擬機器](#existing)

## <a name="new"></a>建立已啟用 R Services 的新 SQL Server 2016 Enterprise 虛擬機器

1. 在 Azure 入口網站中，按一下虛擬機器，然後按一下 [新增]。
2. 選取 [SQL Server 2016 Enterprise 版本]。
3. 設定伺服器名稱和帳戶權限，並選取一個定價方案。
4. 於 VM 設定精靈的步驟 4，在 [SQL Server 設定] 中找出 [R 服務 (進階分析)] 並按一下 [啟用]。
5. 檢閱顯示的摘要進行驗證，並按一下 [確定]。
6. 當虛擬機器準備就緒時，連線至虛擬機器並開啟預先安裝的 SQL Server Management Studio。 R Services 已準備好執行。
7. 若要驗證這一點，您可以開啟新的查詢視窗，並執行簡單的陳述式，如下所示，它使用 R 來產生從 1 到 10 的數字序列。
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. 如果您將從遠端資料科學用戶端連線到執行個體，請視需要完成[額外步驟](#additional-steps)。


## <a name="additional-steps"></a>額外的步驟  

如果預期遠端用戶端存取與遠端的 SQL Server 計算內容伺服器需要一些額外的步驟。

### <a name="firewall"></a>解除封鎖防火牆

根據預設，Azure 虛擬機器上的防火牆包含會封鎖本機 R 使用者帳戶網路存取權的規則。

您必須停用此規則，確保您可以存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從遠端資料科學用戶端的執行個體。  否則，您的 R 程式碼無法執行使用虛擬機器的工作區中的計算內容中，即使其他 R 程式碼會使用 SQL Server 計算內容，不會有問題。

啟用從遠端資料科學用戶端存取 R Services：

1. 在虛擬機器上，開啟 [具有進階安全性的 Windows 防火牆]。
2. 選取 [輸出規則]
3. 停用下列規則︰
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>針對遠端用戶端啟用 ODBC 回呼

如果您預期呼叫伺服器的 R 用戶端將需要發出 ODBC 查詢做為其 R 方案的一部分，您必須確定 Launchpad 可代表遠端用戶端進行 ODBC 呼叫。 若要這樣做，您必須允許 Launchpad 所使用的 SQL 背景工作帳戶登入執行個體。
如需詳細資訊，請參閱[安裝 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。

### <a name="network"></a>新增網路通訊協定

+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會針對用戶端和伺服器電腦之間的連線，以及部分內部連線使用「具名管道」通訊協定。 如果未啟用具名管道，您必須同時在 Azure 虛擬機器以及連線 到伺服器的任何資料科學用戶端上，安裝具名管道並將它啟用。
  
+ 啟用 TCP/IP

  TCP/IP 是 SQL Server R Services 迴路連線的必要項。 如果您收到下列錯誤，請在支援的執行個體的虛擬機器上啟用 TCP/IP:

  「 DBNETLIB;SQL Server 不存在或拒絕存取 」

## <a name="how-to-disable-r-services-on-an-instance"></a>如何停用執行個體上的 R Services

您也可以隨時在現有的虛擬機器上啟用或停用該功能。

1. 開啟虛擬機器刀鋒視窗
2. 按一下 [設定]，並選取 [SQL Server 組態]。

## <a name="existing"></a>將 SQL Server R 服務新增至現有的 SQL Server 2016 Enterprise 虛擬機器

如果您建立 Azure 虛擬機器未包含 R 服務，您可以加入功能，依照下列步驟：

1. 重新執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式，並在精靈的 [伺服器組態] 頁面上新增該功能。
2. 啟用外部指令碼執行，並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱 [安裝 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. (選擇性) 如果遠端指令碼執行需要，請設定 R 背景工作帳戶的資料庫存取權。
   如需詳細資訊，請參閱[安裝 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。
3. (選擇性) 如果您想要允許從遠端資料科學用戶端執行 R 指令碼，請修改 Azure 虛擬機器上的防火牆規則。 如需詳細資訊，請參閱[解除封鎖防火牆](#firewall)。
4. 安裝或啟用必要的網路程式庫。 如需詳細資訊，請參閱[新增網路通訊協定](#network)。

## <a name="related-resources"></a>相關資源

[安裝 SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

