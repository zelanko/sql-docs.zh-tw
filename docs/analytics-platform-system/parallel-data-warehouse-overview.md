---
title: 平行處理資料倉儲元件
description: 此文章說明設備軟體和 Analytics Platform System 的非設備軟體元件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400936"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>平行處理資料倉儲元件-Analytics Platform System
本文說明設備軟體和 Analytics Platform System 的非設備軟體元件。  
  
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
  
## <a name="appliance-software---query-processing-and-user-data-storage"></a><a name="sec1"></a>設備軟體-查詢處理和使用者資料儲存  
  
### <a name="control-node"></a>控制節點  
MPP 引擎  
MPP 引擎是大量平行處理 (MPP) 系統的大腦。 它會執行下列工作：  
  
-   在計算節點上建立平行查詢計劃，並協調平行查詢的執行。  
  
-   儲存和協調所有資料庫的中繼資料和設定資料。  
  
-   管理 SQL Server PDW 資料庫驗證和授權。  
  
-   追蹤硬體和軟體狀態。  
  
### <a name="data-movement-service-dms"></a> (DMS) 的資料移動服務  
 (DMS) 的資料移動服務，屬於 PDW "secret sauce" 的一部分。 它會執行下列工作：  
  
-   將資料傳入和傳出 SQL Server PDW 節點。  
  
-   處理需要在節點之間傳輸資料的查詢作業。  
  
-   藉由優化資料傳送速率來改善查詢效能。  
  
### <a name="admin-console"></a>管理主控台  
管理主控台是一種 web 應用程式，可顯示裝置狀態、健康情況和效能資訊。  
  
### <a name="configuration-manager"></a>Configuration Manager  
Configuration Manager ( # A0) 是設備系統管理員用來設定 Analytics Platform System 的工具。  
  
### <a name="control-node-databases"></a>控制節點資料庫  
SQL Server 管理控制節點上的所有資料庫。  
  
-   Shell 資料庫會管理所有分散式使用者資料庫的中繼資料。  
  
-   TempDB 包含設備上所有使用者臨時表的中繼資料。  
  
-   Master 是控制節點上 SQL Server 的主表。  
  
### <a name="compute-node"></a>計算節點  
計算節點是平行資料處理和儲存單位。 它們具有直接附加的儲存體，並使用 SQL Server 來管理使用者資料。  
  
### <a name="data-movement-service-dms"></a> (DMS) 的資料移動服務  
 (DMS) 的資料移動服務會在每個計算節點上執行，以執行下列動作：  
  
-   在處理平行查詢的過程中，DMS 會將資料傳入和傳出其他電腦節點和控制節點。  
  
-   DMS 會在每個計算節點上執行，以平行方式接收資料載入。 以平行方式將資料直接載入至計算節點的載入伺服器  
  
-   DMS 會將資料從每個計算節點直接傳輸到備份伺服器。  
  
-   DMS 會使用 PolyBase 將資料傳入和傳出外部 Hadoop 叢集或 Azure 儲存體 Blob。  
  
### <a name="compute-node-databases"></a>計算節點資料庫 
每個計算節點都會執行 SQL Server 的實例，以處理查詢及管理使用者資料。  
  
## <a name="appliance-fabric"></a>設備網狀架構  
設備網狀架構會為設備提供作業系統、服務和網路基礎結構。  
  
### <a name="domain-controller"></a>網域控制站  
Active Directory (AD) 網域服務 (DS)   
Analytics Platform System 會在 Analytics Platform System-節點之間執行驗證，並管理 SQL Server PDW Windows 驗證登入的驗證。  
  
DNS 服務  
Windows 功能變數名稱服務 (DNS) 將功能變數名稱解析為 Analytics Platform System 設備的 IP 位址。  
  
### <a name="windows-deployment-service"></a>Windows 部署服務  
Windows 部署服務 (WDS) 將 Windows Server 作業系統部署到設備上。 它會部署在各設備的每部主機和虛擬機器上。  
  
DHCP 服務會建立 IP 位址，如此一來，設備網域內的主機就可以加入設備網路，而不需要預先設定的 IP 位址。  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System 使用虛擬化來達成高可用性。 Virtual Machine Manager 裝載 System Center，以在實體主機上部署作業系統。  
  
Windows Server Update Services (WSUS) 在所有主機和虛擬機器上套用或移除 Windows 更新。  
  
### <a name="windows-server"></a>Windows Server  
設備中的所有主機和虛擬機器都會執行 Windows Server 作業系統。  
  
### <a name="failover-clustering"></a>容錯移轉叢集  
Windows 容錯移轉叢集可讓您在主機失敗的事件中，重新開機被動主機上的進程。  
  
### <a name="storage-spaces"></a>儲存空間  
Windows 儲存空間可將使用者資料管理為一小部分計算節點的存放集區。 如果計算節點失敗，仍可透過群組中的另一個計算節點存取資料。  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server 提供簡單又可靠的虛擬化解決方案。 Analytics Platform System 使用虛擬化來平衡 CPU 資源，並為 PDW 節點和設備網狀架構元件提供高可用性。  
  
## <a name="non-relational-data"></a><a name="sec2"></a>非關聯式資料
PolyBase 技術將 SQL Server PDW 資料與外部 Hadoop 資料整合。 Hadoop 資料可以儲存在這些 Hadoop 資料來源中：  
  
-   Hortonworks Hadoop 散發  
  
-   Hadoop 的 Cloudera 散發  
  
-   儲存在 Azure 儲存體 Blob 上的 HDInsight 資料  
  
## <a name="query-tools"></a>查詢工具   
  
查詢會以 \- 修改過的 transact-sql 來撰寫，以配合查詢的 MPP 本質。 所有查詢都會提交至控制節點，此節點會產生平行查詢計劃，以在計算節點上執行查詢。  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools 會在 Visual Studio 內執行，這是我們建議用來將查詢提交至 SQL Server PDW 的 GUI 工具。 它類似于 SQL Server Management Studio，可讓您流覽物件瀏覽器。  
  
如果您還沒有 Visual Studio，可以免費下載您需要的工具。 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>sqlcmd 命令列查詢工具  
sqlcmd 是用來執行 Transact-sql \- 語句和系統命令的 SQL Server 命令列工具。 它適用于 SQL Server PDW，也是我們建議用來查詢 SQL Server PDW 的命令列工具。 使用 sqlcmd，您可以 \- 從命令列、批次檔或 Windows PowerShell，以互動方式執行 transact-sql 語句。  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
您可以使用 Integration Services 來查詢 SQL Server PDW。 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>連結的伺服器  
藉由使用 SQL Server 連結伺服器連接，您可以使用 SQL Server 將 Transact-sql \- 語句提交至 SQL Server PDW。 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>商業智慧工具
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW 是 Analysis Services 資料庫和 Excel PowerPivot 模型的有效資料來源。 使用 OLE DB 提供者，您可以將 Analysis Services cube 設定為使用多維度線上分析處理 (MOLAP) 或關聯式線上分析處理 (ROLAP) 儲存體。  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>報表產生器  
您可以使用 SQL Server PDW 做為您針對 Reporting Services 使用 SQL Server Report Builder 所開發之報表的 SQL Server 資料來源。 您也可以使用 SQL Server PDW 作為報表模型的 SQL Server 來源。 藉由使用報表管理員或報表伺服器 API，您可以從 SQL Server PDW 資料庫產生模型。  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot for Excel  
您可以使用 PowerPivot for Excel （可大幅擴充 Excel 的資料分析功能的免費下載）連接到 SQL Server PDW。  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>載入工具 
  
### <a name="integration-services"></a>Integration Services  
安裝 PDW 特定的目的地介面卡，讓您可以使用 SQL ServerIntegration 服務將資料載入 SQL Server PDW。  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>dwloader 命令列載入器  
dwloader 是一種命令列載入工具，可從您的載入伺服器以平行方式將資料載入 SQL Server PDW 的計算節點。 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>適用于 Hadoop 整合的 PolyBase  
使用 PolyBase 技術，您可以將 Hadoop 叢集的非關聯式資料載入 SQL Server PDW 中的關聯式資料表。 Hadoop 資料可以位於外部 Hadoop 叢集中或 Azure 儲存體 Blob。  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>資料庫備份和還原  
SQL Server PDW 使用 Transact-sql 資料庫備份和還原命令，以平行方式將使用者資料庫備份和還原到備份伺服器。 SQL Server PDW 將備份寫入 Windows 檔案共用中的目錄，然後同樣還原 Windows 檔案共用的資料。  
  
如需詳細資訊，請參閱 [規劃備份和載入硬體](backup-and-loading-hardware.md) 和 [備份與還原總覽](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>遠端資料表複製  
遠端資料表複製功能可讓您將資料表從 SQL Server PDW 資料庫複製到遠端 (非設備) SMP SQL Server 資料庫。 這會啟用 SQL Server PDW 的中樞和輪輻案例。  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>監視  
Analytics Platform System 有數種方式可監視設備活動  
  
### <a name="admin-console"></a>管理主控台  
系統管理主控台可讓您查看設備健全狀況的目前狀態。 這會以 web 應用程式的形式在控制項節點上執行，並可透過 HTTPs 存取。  
  
如需詳細資訊，請參閱 [使用管理主控台 &#40;Analytics Platform System 監視設備&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>系統檢視表  
管理主控台是以系統檢視查詢為基礎。 您可以個別查詢系統檢視，以取得所需的特定資訊片段。  

如需詳細資訊，請參閱 [使用系統檢視 &#40;Analytics Platform System 監視設備&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
SQL Server PDW 有 System Center Operations Manager 的 (SCOM) 管理元件。 

若要為 SCOM 設定設備，請參閱 [使用 System Center Operations Manager &#40;Analytics Platform System 監視設備&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
