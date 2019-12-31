---
title: 平行處理資料倉儲元件
description: 這篇文章說明分析平臺系統的設備軟體和非設備軟體元件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400936"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>平行處理資料倉儲元件-Analytics Platform System
本文說明分析平臺系統的設備軟體和非設備軟體元件。  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![平行處理資料倉儲軟體](media/parallel-data-warehouse-software.png "平行處理資料倉儲軟體")  
  
## <a name="sec1"></a>設備軟體-查詢處理和使用者資料儲存  
  
### <a name="control-node"></a>控制節點  
MPP 引擎  
MPP 引擎是大規模平行處理（MPP）系統的大腦。 它具有下列功能：  
  
-   建立平行查詢計劃，並協調計算節點上的平行查詢執行。  
  
-   儲存和協調所有資料庫的中繼資料和設定資料。  
  
-   管理 SQL Server PDW 資料庫驗證和授權。  
  
-   追蹤硬體和軟體狀態。  
  
### <a name="data-movement-service-dms"></a>資料移動服務（DMS）  
資料移動服務（DMS）是 PDW 「秘密 sauce」的一部分。 它具有下列功能：  
  
-   將資料傳輸到 SQL Server PDW 的節點，以及從其傳出。  
  
-   處理需要在節點之間傳送資料的查詢作業。  
  
-   藉由優化資料傳送速率來提升查詢效能。  
  
### <a name="admin-console"></a>管理主控台  
管理主控台是一種 web 應用程式，可提供設備狀態、健康情況和效能資訊。  
  
### <a name="configuration-manager"></a>組態管理員  
Configuration Manager （dwconfig .exe）是設備系統管理員用來設定分析平臺系統的工具。  
  
### <a name="control-node-databases"></a>控制節點資料庫  
SQL Server 管理控制節點上的所有資料庫。  
  
-   Shell 資料庫會管理所有分散式使用者資料庫的中繼資料。  
  
-   TempDB 包含設備上所有使用者臨時表的中繼資料。  
  
-   Master 是控制節點上 SQL Server 的主資料表。  
  
### <a name="compute-node"></a>計算節點  
計算節點是平行處理資料和儲存單位。 它們具有直接連接的儲存體，並使用 SQL Server 來管理使用者資料。  
  
### <a name="data-movement-service-dms"></a>資料移動服務（DMS）  
資料移動服務（DMS）會在每個計算節點上執行，以進行下列動作：  
  
-   在處理平行查詢的過程中，DMS 會在其他電腦節點與控制節點之間傳輸資料。  
  
-   DMS 在每個計算節點上執行時，會以平行方式接收資料載入。 資料會以平行方式從載入伺服器直接載入至計算節點  
  
-   DMS 會將每個計算節點的資料直接傳輸到備份伺服器。  
  
-   使用 PolyBase 時，DMS 會將資料傳輸至外部 Hadoop 叢集或 Azure 儲存體 Blob。  
  
### <a name="compute-node-databases"></a>計算節點資料庫 
每個計算節點都會執行 SQL Server 的實例，以處理查詢和管理使用者資料。  
  
## <a name="appliance-fabric"></a>設備網狀架構  
設備網狀架構提供設備的作業系統、服務和網路基礎結構。  
  
### <a name="domain-controller"></a>網域控制站  
Active Directory （AD）網域服務（DS）  
Analytics Platform System 會在分析平臺系統節點之間執行驗證，並管理 SQL Server PDW Windows 驗證登入的驗證。  
  
DNS 服務  
Windows 功能變數名稱服務（DNS）會將功能變數名稱解析為分析平臺系統裝置的 IP 位址。  
  
### <a name="windows-deployment-service"></a>Windows 部署服務  
Windows 部署服務（WDS）會將 Windows Server 作業系統部署到設備上。 它會部署在跨應用裝置的每部主機和虛擬機器上。  
  
DHCP 服務會建立 IP 位址，如此一來，設備網域內的主機就可以加入設備網路，而不需要預先設定的 IP 位址。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System 使用虛擬化來達到高可用性。 Virtual Machine Manager 會主控 System Center，以在實體主機上部署作業系統。  
  
Windows Server Update Services （WSUS）在所有主機和虛擬機器上套用或移除 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
設備中的所有主機和虛擬機器都執行 Windows Server 作業系統。  
  
### <a name="failover-clustering"></a>容錯移轉叢集  
Windows 容錯移轉叢集可以在主機失敗時，重新開機被動主機上的進程。  
  
### <a name="storage-spaces"></a>儲存空間  
Windows 儲存空間會將使用者資料管理為一小組計算節點的儲存集區。 如果計算節點失敗，仍然可以透過群組中的另一個計算節點來存取資料。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-v Server 提供簡單又可靠的虛擬化解決方案。 分析平臺系統會使用虛擬化來平衡 CPU 資源，並為 PDW 節點和設備網狀架構元件提供高可用性。  
  
## <a name="sec2"></a>非關聯式資料
PolyBase 技術將 SQL Server PDW 資料與外部 Hadoop 資料整合在一起。 Hadoop 資料可以儲存在下列任何 Hadoop 資料來源上：  
  
-   Hortonworks Hadoop 散發  
  
-   Hadoop 的 Cloudera 散發  
  
-   儲存在 Azure 儲存體 Blob 上的 HDInsight 資料  
  
## <a name="query-tools"></a>查詢工具   
  
查詢會以已修改\-的 transact-sql 來撰寫，以符合查詢的 MPP 性質。 所有查詢都會提交至控制節點，其會產生平行查詢計劃，以在計算節點上執行查詢。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server 資料工具 (SSDT)  
SQL Server Data Tools 會在 Visual Studio 內執行，而且是我們建議用來將查詢提交至 SQL Server PDW 的 GUI 工具。 它類似于 SQL Server Management Studio，可讓您流覽物件瀏覽器。  
  
如果您尚未 Visual Studio，您可以免費下載所需的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令列查詢工具  
sqlcmd 是用來執行 Transact-sql\-語句和系統命令的 SQL Server 命令列工具。 它適用于 SQL Server PDW，而且是我們建議用來查詢 SQL Server PDW 的命令列工具。 使用 sqlcmd，您可以從\-命令列、批次檔或 Windows PowerShell，以互動方式執行 transact-sql 語句。  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
您可以使用 Integration Services 來查詢 SQL Server PDW。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>連結的伺服器  
藉由使用 SQL Server 連結的伺服器連接，您可以使用 SQL Server 將 Transact-sql\-語句提交至 SQL Server PDW。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商業智慧工具
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW 是 Analysis Services 資料庫和 Excel PowerPivot 模型的有效資料來源。 您可以使用 OLE DB 提供者，將 Analysis Services cube 設定為使用多維度線上分析處理（MOLAP）或關聯式線上分析處理（ROLAP）儲存。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>報表產生器  
您可以使用 SQL Server PDW 做為使用 SQL Server 報表產生器針對 Reporting Services 所開發之報表的 SQL Server 資料來源。 您也可以使用 SQL Server PDW 做為報表模型的 SQL Server 來源。 藉由使用報表管理員或報表伺服器 API，您可以從 SQL Server PDW 資料庫產生模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
您可以使用 PowerPivot for Excel 連接到 SQL Server PDW，這是一項免費下載，可大幅擴充 Excel 的資料分析功能。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>載入工具 
  
### <a name="integration-services"></a>Integration Services  
安裝 PDW 特定的目的地介面卡，可讓您使用 SQL ServerIntegration 服務將資料載入 SQL Server PDW。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令列載入器  
dwloader 是命令列載入工具，可從您的載入伺服器以平行方式將資料載入 SQL Server PDW 計算節點。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>適用于 Hadoop 整合的 PolyBase  
使用 PolyBase 技術，您可以將非關聯式資料從 Hadoop 叢集載入 SQL Server PDW 中的關聯式資料表。 Hadoop 資料可以位於外部 Hadoop 叢集或 Azure 儲存體 Blob 中。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>資料庫備份和還原  
SQL Server PDW 使用 Transact-sql 資料庫備份和還原命令，以平行方式備份和還原備份伺服器的使用者資料庫。 SQL Server PDW 會將備份寫入 Windows 檔案共用中的目錄，然後同樣還原 Windows 檔案共用中的資料。  
  
如需詳細資訊，請參閱[規劃備份和載入硬體](backup-and-loading-hardware.md)和[備份和還原總覽](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>遠端資料表複本  
遠端資料表複製功能可讓您將資料表從 SQL Server PDW 資料庫複製到遠端（非應用裝置） SMP SQL Server 資料庫。 這會啟用 SQL Server PDW 的中樞和輪輻案例。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>監視  
Analytics Platform System 有數種方式可監視設備活動  
  
### <a name="admin-console"></a>管理主控台  
系統管理主控台可讓您查看設備健全狀況的目前狀態。 這會在控制節點上以 web 應用程式的形式執行，並可透過 HTTPs 存取。  
  
如需詳細資訊，請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系統檢視  
管理主控台是以系統檢視查詢為基礎。 您可以個別查詢系統檢視，以取得所需的特定資訊片段。  

如需詳細資訊，請參閱[使用系統檢視來監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
有適用于 SQL Server PDW 的 System Center Operations Manager （SCOM）管理元件。 

若要設定 SCOM 的設備，請參閱[使用 System Center Operations Manager &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
