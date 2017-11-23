---
title: "平行資料倉儲概觀"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "本主題說明裝置軟體和 Analytics Platform System 的非裝置軟體元件。"
ms.date: 01/05/2017
ms.topic: article
ms.assetid: db0c4a43-a66d-4c44-ab91-791c5785f71c
caps.latest.revision: "20"
ms.openlocfilehash: 587b1ce6720fc07d9ac24edde2c5b8cc2b30c89f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="parallel-data-warehouse-overview"></a>平行資料倉儲概觀
本主題說明裝置軟體和 Analytics Platform System 的非裝置軟體元件。  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![平行資料倉儲軟體](media/parallel-data-warehouse-software.png "Parallel Data Warehouse 軟體")  
  
## <a name="sec1"></a>應用裝置軟體 – 查詢處理和使用者資料存放區  
  
### <a name="control-node"></a>控制節點  
MPP 引擎  
MPP 引擎是大量平行處理 (MPP) 系統的大腦。 它會執行下列工作：  
  
-   建立平行查詢計劃，並協調計算節點上的同時執行查詢。  
  
-   儲存並協調所有資料庫的中繼資料和設定資料。  
  
-   管理 SQL Server PDW 資料庫驗證和授權。  
  
-   追蹤硬體和軟體的狀態。  
  
### <a name="data-movement-service-dms"></a>資料移動服務 (DMS)  
資料移動服務 (DMS) 是 「 推手"PDW 的一部分。 它會執行下列工作：  
  
-   傳輸資料與 SQL Server PDW 節點。  
  
-   處理查詢需要在節點之間傳輸資料的作業。  
  
-   改善查詢效能最佳化的資料傳輸速度。  
  
### <a name="admin-console"></a>管理主控台  
系統管理員主控台是 web 應用程式所呈現的應用裝置狀態、 健全狀況和效能資訊。  
  
### <a name="configuration-manager"></a>組態管理員  
Configuration Manager (dwconfig.exe)，是應用裝置系統管理員用來設定 Analytics Platform System 的工具。  
  
### <a name="control-node-databases"></a>控制節點資料庫  
SQL Server 管理的所有資料庫上的控制節點。  
  
-   Shell 資料庫管理的所有分散式的使用者資料庫的中繼資料。  
  
-   TempDB 包含跨應用裝置的所有使用者的暫存資料表的中繼資料。  
  
-   主機是適用於 SQL Server 上的控制項節點主要資料表。  
  
### <a name="compute-node"></a>計算節點  
計算節點是平行的資料處理和儲存體單位。 它們具有直接連結存放裝置，並使用 SQL Server 來管理使用者資料。  
  
### <a name="data-movement-service-dms"></a>資料移動服務 (DMS)  
資料移動服務 (DMS) 可執行下列每個計算節點上執行：  
  
-   處理平行查詢的一部分，DMS 傳輸資料與其他電腦節點及控制節點。  
  
-   DMS，每個計算節點上，執行會以平行方式接收資料載入。 用於運算節點載入伺服器直接從平行載入資料  
  
-   DMS 會將資料從每個計算節點傳送到備份伺服器。  
  
-   使用 PolyBase，DMS 可以傳輸資料給予或來自外部的 Hadoop 叢集中或 HDInsight 區域應用裝置上。  
  
### <a name="compute-node-databases"></a>計算節點的資料庫 
每個計算節點執行處理查詢和管理使用者資料的 SQL Server 執行的個體。  
  
## <a name="appliance-fabric"></a>應用裝置網狀架構  
應用裝置網狀架構會提供應用裝置的作業系統、 服務和網路基礎結構。  
  
### <a name="domain-controller"></a>網域控制站  
Active Directory (AD) 網域服務 (DS)  
Analytics Platform System 執行 Analytics Platform System 節點之間的驗證，並管理的 SQL Server PDW Windows 驗證登入驗證。  
  
DNS 服務  
Windows 網域名稱服務 (DNS) 解析網域名稱 Analytics Platform System 應用裝置的 IP 位址。  
  
### <a name="windows-deployment-service"></a>Windows 部署服務  
Windows 部署服務 (WDS) 部署 Windows Server 作業系統至應用裝置。 應用裝置上部署每個主機和虛擬機器上。  
  
DHCP 服務建立 IP 位址，好讓應用裝置網域內的主機可以將應用裝置網路，而不需要預先設定的 IP 位址。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System 使用虛擬化，來達到高可用性。 Virtual Machine Manager 主控 System Center 部署在實體主機上的作業系統。  
  
Windows Server Update Services (WSUS) 來套用或移除主機和虛擬機器的所有 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
所有主機和應用裝置中的虛擬機器執行 Windows Server 作業系統。  
  
### <a name="failover-clustering"></a>容錯移轉叢集  
Windows 容錯移轉叢集提供的主機失敗，請重新啟動被動的主機上的處理序的能力。  
  
### <a name="storage-spaces"></a>儲存空間  
Windows 儲存空間做為計算節點的一小群儲存集區管理使用者資料。 如果計算節點失敗時，資料是仍然可以存取透過另一個群組中的計算節點。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft HYPER-V Server 提供的簡單又可靠的虛擬化解決方案。 Analytics Platform System 會使用虛擬，以平衡 CPU 資源，並提供高可用性的 PDW 節點和應用裝置網狀架構元件。  
  
## <a name="sec2"></a>非關聯式資料
PolyBase 技術，將 SQL Server PDW 資料與外部的 Hadoop 資料相整合。 Hadoop 資料可以儲存在任何這些 Hadoop 資料來源：  
  
-   Linux 或 Windows Server 的 Hortonworks  
  
-   在 Linux 上的 Cloudera  
  
-   HDInsight AP 上執行  
  
-   HDInsight 資料儲存在 Azure 儲存體 Blob  
  
## <a name="query-tools"></a>查詢工具   
  
查詢以 Transact-sql\-SQL 修改以符合 MPP 查詢的本質。 所有的查詢會提交到產生的計算節點上執行查詢的平行查詢計畫的控制節點。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools 會在 Visual Studio 內執行且提交到 SQL Server PDW 查詢我們建議的 GUI 工具。 它是類似於 SQL Server Management Studio 可讓您透過 [物件總管] 瀏覽。  
  
如果您還沒有 Visual Studio，您可以下載您需要免費的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令列查詢工具  
sqlcmd 是 SQL Server 命令列工具執行 Transact\-SQL 陳述式及系統命令。 它適用於 SQL Server PDW，我們建議的命令列工具，查詢 SQL Server PDW。您可以使用 sqlcmd 執行 Transact-sql\-以互動方式從命令列中，以批次檔，或從 Windows PowerShell 的 SQL 陳述式。  
  
<!-- MISSING LINKS

If you don’t have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
您可以查詢 SQL Server PDW 使用 Integration Services。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>連結的伺服器  
使用 SQL Server 連結伺服器連接，您可以使用 SQL Server 提交 Transact-sql\-SQL Server PDW 的 SQL 陳述式。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商業智慧工具
  
Analysis Services  
SQL Server PDW 是 Analysis Services 資料庫和 Excel PowerPivot 模型的有效資料來源。 使用 OLE DB 提供者，您可以設定為使用多維度線上分析處理 (MOLAP) 或關聯式線上分析處理 (ROLAP) 儲存體的 Analysis Services cube。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>報表產生器  
您可以使用 SQL Server PDW 做為 SQL Server 資料來源，您使用 SQL Server 報表產生器開發 Reporting services 的報表。 您也可以使用做為 SQL Server 來源的 SQL Server PDW 的報表模型。 使用報表管理員或報表伺服器應用程式開發介面，您可以從 SQL Server PDW 資料庫產生模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
您可以連接到 SQL Server PDW 與 PowerPivot for Excel，大幅擴充了 Excel 的資料分析功能的免費下載。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>載入的工具 
  
### <a name="integration-services"></a>Integration Services  
安裝可讓您使用 SQL ServerIntegration 服務將資料載入 SQL Server PDW PDW 特定目的地配接器。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令列載入器  
dwloader 是載入的命令列工具，載入伺服器中以平行方式的資料載入到 SQL Server PDW 運算節點。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase Hadoop 整合  
使用 PolyBase 技術，您可以載入非關聯式資料從 Hadoop 叢集 SQL Server PDW 中的關聯式資料表。 可以位於 Hadoop 資料，在 Hadoop 叢集上 AP，HDI 區域外部或 Azure 儲存體 Blob。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>資料庫備份和還原  
SQL Server PDW 使用 Transact\-SQL 資料庫備份和還原命令來備份和還原使用者資料庫，以平行方式，與備份的伺服器。 SQL Server PDW 備份寫入 Windows 檔案共用的目錄，然後同樣地，會還原資料從 Windows 檔案共用。  
  
如需詳細資訊，請參閱[規劃備份及載入硬體](backup-and-loading-hardware.md)和[備份及還原概觀](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>遠端資料表複製  
遠端資料表複製功能可讓您將資料表從 SQL Server PDW 資料庫複製到遠端 （非應用裝置） SMP SQL Server 資料庫。 這樣可以中樞和支點為 SQL Server PDW。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>監視  
Analytics Platform System 有數種方式來監視應用裝置活動  
  
### <a name="admin-console"></a>管理主控台  
在管理主控台可讓您檢視有關應用裝置健康情況的目前狀態。 此 web 應用程式的控制節點上執行而且可透過 https。  
  
如需詳細資訊，請參閱[使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系統檢視表  
系統管理員主控台會根據系統檢視查詢。 您可以查詢系統檢視表，才能取得特定的片段，您需要的資訊。  

如需詳細資訊，請參閱[監視所使用的系統檢視 &#40; 應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
沒有 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理組件。 

若要設定 SCOM 應用裝置，請參閱[監視使用 System Center Operations Manager &#40; 應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
