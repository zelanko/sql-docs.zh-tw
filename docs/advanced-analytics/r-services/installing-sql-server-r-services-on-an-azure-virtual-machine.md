---
title: "在 Azure 虛擬機器上安裝 SQL Server R 服務 | Microsoft Docs"
ms.custom: ""
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 在 Azure 虛擬機器上安裝 SQL Server R 服務
 
如果您部署 Azure 虛擬機器，其中包含 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，您現在可以選取 R 服務做為 VM 建立時，要加入至執行個體的功能。 



+ [建立新的 VM 與 SQL Server 2016 和 R 服務](#new)
+ [將 R 服務新增至現有的虛擬機器使用 SQL Server 2016](#existing)

## <a name="a-namenewacreate-a-new-sql-server-2016-enterprise-virtual-machine-with-r-services-enabled"></a><a name="new"></a>使用 R 啟用服務，才能建立新的 SQL Server 2016 企業虛擬機器

1. 在 Azure 入口網站中，按一下虛擬機器，然後按一下 [新增]。
2. 選取 SQL Server 2016 企業版。
3. 設定伺服器名稱和帳戶權限，以及選取的定價方案。
4. 步驟 4 中的 VM 上安裝精靈，在 **SQL Server 設定**, ，找出 **R 服務 （進階分析）** 按一下 **啟用**。
5. 檢閱摘要進行驗證，並按一下 [顯示 **確定**。
6. 準備虛擬機器時，連接到它，並開啟 SQL Server Management Studio，這是預先安裝。 R 服務已準備好執行。 
7. 若要驗證這一點，您可以開啟新的查詢視窗，並執行簡單的陳述式，如下列步驟，使用 R 來產生一串數字為 1 到 10。
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. 如果您將會從遠端資料科學用戶端連線到執行個體，請先完成 [額外的步驟](#additional-steps) 視。


## <a name="additional-steps"></a>額外的步驟  

如果您希望遠端用戶端存取伺服器做為遠端 SQL Server 計算內容使用 R 服務可能需要一些額外的步驟。

### <a name="a-namefirewallaunblock-the-firewall"></a><a name="firewall"></a>解除封鎖防火牆  
  
您必須變更以確保您可以存取虛擬機器上的防火牆規則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從遠端資料科學用戶端的執行個體。  否則，您可能無法使用需要的內容會使用虛擬機器的工作區的計算。 

根據預設，Azure 虛擬機器上的防火牆會包括封鎖網路 R 的本機使用者帳戶的存取規則。  
  
若要啟用 R 服務從遠端資料科學的用戶端存取︰
1. 虛擬機器上，開啟 [具有進階安全性的 Windows 防火牆。
2. 選取 **輸出規則**
3. 停用下列規則︰  
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`  
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>針對遠端用戶端啟用 ODBC 回呼

如果您預期的 R 用戶端呼叫伺服器都必須發出 ODBC 查詢 R 解決方案的一部分，您必須確定 [啟動列] 可讓 ODBC 呼叫代表遠端用戶端。 若要這樣做，您必須允許啟動列用來登入執行個體的 SQL 工作者帳戶。
如需詳細資訊，請參閱 [設定安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。 

### <a name="a-namenetworkaadd-network-protocols"></a><a name="network"></a>新增網路通訊協定  
  
+ 啟用具名管道
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會使用具名管道通訊協定，用戶端和伺服器電腦之間的連線，以及某些內部連線。 如果未啟用具名管道，您必須安裝並啟用它，這兩個 Azure 虛擬機器，以及任何連線到伺服器的資料科學用戶端。  
  
+ 啟用 TCP/IP

  TCP/IP 是回送連接到 SQL Server R Services 的必要項。 如果您收到下列錯誤，則在支援的執行個體 DBNETLIB; 在虛擬機器上啟用 TCP/IPSQL Server 不存在或拒絕存取。

## <a name="how-to-disable-r-services-on-an-instance"></a>如何停用 R 的服務執行個體上

您也可以啟用或停用現有的虛擬機器上的功能，在任何時間。 

1. 開啟虛擬機器分頁
2. 按一下 [ **設定**, ，然後選取 **SQL Server 組態**。


## <a name="a-nameexistingaadd-sql-server-r-services-to-an-existing-sql-server-2016-enterprise-virtual-machine"></a><a name="existing"></a>將 SQL Server R 服務新增至現有的 SQL Server 2016 Enterprise 虛擬機器

如果您使用 SQL Server 2016 不含 R 服務建立 Azure VM，您可依照下列步驟來新增功能︰

1. 重新執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定，並在 [新增功能 **伺服器組態** 精靈頁面。
2. 啟用外部指令碼執行並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱 < 請參閱 [設定安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。
3. （選擇性）如果需要遠端指令碼執行，請設定 R 背景工作帳戶的資料庫存取權。
   如需詳細資訊，請參閱 [設定安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。 
3. （選擇性）如果您想要允許從遠端資料科學的用戶端的 R 指令碼執行，請修改 Azure 的虛擬機器上的防火牆規則。 如需詳細資訊，請參閱 [解除封鎖防火牆](#firewall)。
4. 安裝或啟用所需的網路程式庫。 如需詳細資訊，請參閱 [新增網路通訊協定](#network)。

## <a name="see-also"></a>另請參閱
[設定 Sql Server R 服務](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)