---
title: 平行資料倉儲元件-Analytics Platform System |Microsoft Docs
description: 此文章說明裝置軟體和 Analytics Platform System 的非應用裝置的軟體元件。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 99d3317f25af947f042d43fdd64e4cad334ca51f
ms.sourcegitcommit: 974c95fdda6645b9bc77f1af2d14a6f948fe268a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2018
ms.locfileid: "37890999"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>平行資料倉儲元件-Analytics Platform System
這篇文章說明裝置軟體和 Analytics Platform System 的非應用裝置的軟體元件。  
  
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
  
## <a name="sec1"></a>設備軟體 – 查詢處理和儲存使用者資料  
  
### <a name="control-node"></a>控制節點  
MPP 引擎  
MPP 引擎是大量平行處理 (MPP) 系統的大腦。 它會執行下列工作：  
  
-   建立平行查詢計劃，並協調計算節點上的平行查詢執行。  
  
-   儲存並協調所有資料庫的中繼資料和組態資料。  
  
-   管理 SQL Server PDW database 驗證和授權。  
  
-   會追蹤硬體和軟體的狀態。  
  
### <a name="data-movement-service-dms"></a>資料移動服務 (DMS)  
資料移動服務 (DMS) 是 「 獨家 」 的 PDW 的一部分。 它會執行下列工作：  
  
-   將資料從 SQL Server PDW 節點來回傳輸。  
  
-   處理查詢需要在節點之間的資料傳輸作業。  
  
-   可改善查詢效能最佳化的資料傳輸速度。  
  
### <a name="admin-console"></a>管理主控台  
系統管理員主控台是提出應用裝置狀態、 健全狀況和效能資訊的 web 應用程式。  
  
### <a name="configuration-manager"></a>組態管理員  
Configuration Manager (dwconfig.exe)，是應用裝置系統管理員用來設定 Analytics Platform System 的工具。  
  
### <a name="control-node-databases"></a>控制節點資料庫  
SQL Server 可以管理所有在控制節點上的資料庫。  
  
-   Shell 資料庫管理分散式的使用者的所有資料庫的中繼資料。  
  
-   TempDB 包含跨設備的所有使用者的暫存資料表的中繼資料。  
  
-   主機是在控制節點上 SQL Server 的主要資料表。  
  
### <a name="compute-node"></a>計算節點  
計算節點是平行資料處理和儲存體單位。 它們具有直接連結存放裝置，並使用 SQL Server 來管理使用者資料。  
  
### <a name="data-movement-service-dms"></a>資料移動服務 (DMS)  
執行下列每個計算節點上，執行資料移動服務 (DMS):  
  
-   處理平行查詢的過程，DMS 會將其他電腦節點和控制節點的資料傳輸。  
  
-   DMS，每個計算節點上，執行會以平行方式接收資料載入。 直接從伺服器載入至計算節點的平行載入資料  
  
-   DMS 會直接往備份伺服器，將資料傳輸每個計算節點。  
  
-   採用 PolyBase，DMS 來回傳輸資料從外部 Hadoop 叢集或 Azure 儲存體 Blob。  
  
### <a name="compute-node-databases"></a>計算節點資料庫 
每個計算節點執行處理查詢和管理使用者資料的 SQL Server 執行的個體。  
  
## <a name="appliance-fabric"></a>設備的網狀架構  
設備的網狀架構會提供作業系統、 服務和網路基礎結構設備。  
  
### <a name="domain-controller"></a>網域控制站  
Active Directory (AD) 網域服務 (DS)  
Analytics Platform System 執行 Analytics Platform System 節點之間的驗證，並管理的 SQL Server PDW Windows 驗證登入驗證。  
  
DNS 服務  
Windows 網域名稱服務 (DNS) 解析 IP 位址，Analytics Platform System appliance 的網域名稱。  
  
### <a name="windows-deployment-service"></a>Windows 部署服務  
Windows 部署服務 (WDS) Windows Server 將作業系統部署至應用裝置。 跨設備，它會部署在每個主機和虛擬機器。  
  
DHCP 服務會建立 IP 位址，以便設備網域內的主機可以聯結應用裝置網路，而不需要預先設定的 IP 位址。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System 會使用虛擬化來達成高可用性。 Virtual Machine Manager 主控 System Center 部署在實體主機上的作業系統。  
  
Windows Server Update Services (WSUS) 即可套用或移除所有主機和虛擬機器的 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
所有主機和設備中的虛擬機器執行 Windows Server 作業系統。  
  
### <a name="failover-clustering"></a>容錯移轉叢集  
Windows 容錯移轉叢集提供的主機失敗，請重新啟動被動的主機上的處理序的能力。  
  
### <a name="storage-spaces"></a>儲存空間  
Windows 儲存空間做為一小群的計算節點的儲存體集區管理使用者資料。 如果計算節點失敗，資料是仍然可以存取透過群組中的另一個計算節點。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft HYPER-V Server 提供既簡單又可靠的虛擬化解決方案。 Analytics Platform System 會使用虛擬，來平衡 CPU 資源，並提供高可用性的 PDW 節點和設備的網狀架構元件。  
  
## <a name="sec2"></a>非關聯式資料
PolyBase 技術整合 SQL Server PDW 資料與外部 Hadoop 資料。 Hadoop 資料可以儲存在任何這些 Hadoop 資料來源：  
  
-   Hortonworks Hadoop 散發套件  
  
-   Cloudera Hadoop 分布  
  
-   儲存在 Azure 儲存體 Blob 上的 HDInsight 資料  
  
## <a name="query-tools"></a>查詢工具   
  
查詢以 Transact-sql\-SQL 修改以符合查詢的 MPP 本質。 所有的查詢會提交到控制節點，會產生平行查詢計畫中的計算節點之間執行查詢。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools 在 Visual Studio 內執行，並是我們建議的 GUI 工具，提交至 SQL Server PDW 查詢。 它是類似於 SQL Server Management Studio 可讓您透過 [物件總管] 瀏覽。  
  
如果您還沒有 Visual Studio，您可以下載您需要免費的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令列查詢工具  
sqlcmd 是 SQL Server 命令列工具執行 Transact\-SQL 陳述式及系統命令。 它適用於 SQL Server PDW，我們建議的命令列工具，可查詢 SQL Server PDW。 您可以使用 sqlcmd 執行 Transact-sql\-以互動方式從命令列中，以批次檔，或從 Windows PowerShell 的 SQL 陳述式。  
  
<!-- MISSING LINKS

If you don’t have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
您可以使用 Integration Services，查詢 SQL Server PDW。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>連結的伺服器  
藉由使用 SQL Server 連結伺服器連接，您可以使用 SQL Server 提交 Transact-sql\-SQL Server pdw 的 SQL 陳述式。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商業智慧工具
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW 是 Analysis Services 資料庫和 Excel PowerPivot 模型的有效資料來源。 使用 OLE DB 提供者，您可以設定為使用多維度線上分析處理 (MOLAP) 或關聯式線上分析處理 (ROLAP) 儲存體的 Analysis Services cube。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>報表產生器  
您可以使用 SQL Server PDW 做為 SQL Server 資料來源，您是使用 SQL Server 報表產生器來進行開發 Reporting services 的報表。 您也可以使用做為 SQL Server 來源的 SQL Server PDW 的報表模型。 使用報表管理員或報表伺服器的 API，您可以從 SQL Server PDW 資料庫產生模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
您可以連接到 SQL Server PDW 與 PowerPivot for Excel，大幅擴充了 Excel 的資料分析功能的免費下載。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>正在載入工具 
  
### <a name="integration-services"></a>Integration Services  
安裝特定 PDW 目的地配接器可讓您將 SQL ServerIntegration 服務將資料載入 SQL Server PDW。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令列載入器  
dwloader 是一種命令列載入工具，從載入伺服器的資料平行載入到 SQL Server PDW 的計算節點。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase Hadoop 整合  
透過 PolyBase 技術，您可以載入非關聯式資料與 Hadoop 叢集 SQL Server PDW 中的關聯式資料表。 Hadoop 資料可以位於外部 Hadoop 叢集中，或在 Azure 儲存體 Blob 中。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>資料庫備份和還原  
SQL Server PDW 使用 Transact SQL database 備份和還原命令來備份和還原備份的伺服器中的使用者資料庫，以平行方式。 SQL Server PDW 備份寫入 Windows 檔案共用中的目錄，並同樣地將資料還原從 Windows 檔案共用。  
  
如需詳細資訊，請參閱 <<c0> [ 規劃備份及載入硬體](backup-and-loading-hardware.md)和[備份與還原概觀](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>遠端資料表複製  
遠端資料表複製功能可讓您將資料表從 SQL Server PDW 資料庫複製到遠端的 （非應用裝置） SMP SQL Server 資料庫。 這樣可以中樞和支點為 SQL Server PDW。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>監視  
Analytics Platform System 有數種方式來監視設備活動  
  
### <a name="admin-console"></a>管理主控台  
系統管理員主控台可讓您檢視應用裝置健康情況相關的目前狀態。 這會在控制節點上執行做為 web 應用程式，並透過 https，則可存取。  
  
如需詳細資訊，請參閱 <<c0> [ 使用管理主控台來監視設備&#40;Analytics Platform System&#41;</c0>](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系統檢視表  
系統管理員主控台為基礎系統檢視查詢。 您可以查詢系統檢視表，才能取得特定的一段您所需要的資訊。  

如需詳細資訊，請參閱 <<c0> [ 監視設備所使用的系統檢視表&#40;Analytics Platform System&#41;</c0>](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
有適用於 SQL Server PDW 的 System Center Operations Manager (SCOM) 管理組件。 

若要設定 SCOM 應用裝置，請參閱[監視設備使用 System Center Operations manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
