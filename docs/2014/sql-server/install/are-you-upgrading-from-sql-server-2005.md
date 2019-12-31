---
title: 從 SQL Server 2005 升級嗎？ | Microsoft Docs
ms.custom: ''
ms.date: 12/15/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d50a66a-1845-4116-8b3a-7b5a2eeb78e6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d5e44dac2201953858f06d834b1831aa1a22fe3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247275"
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>從 SQL Server 2005 升級嗎？
  由於對 SQL Server 2005 的延伸支援即將結束，因此建議您立即升級到新版 SQL Server 及 Azure SQL Database。 透過升級，您能夠維護安全性與相容性、達到突破性的效能，並將資料平台基礎結構最佳化。  
  
 如需詳細資訊、指引及取得工具以規劃及自動化您的升級或移轉，請參閱 [不再支援 SQL Server 2005](https://www.microsoft.com/server-cloud/products/sql-server-2005/)。  
  
## <a name="why-upgrade"></a>為何要升級？  
  
> [!IMPORTANT]  
>  SQL Server 2005 的延長支援將於 2016 年 4 月 12 日結束。 若您在 2016 年 4 月 12 日之後繼續使用 SQL Server 2005，將不會再收到任何安全性更新。  
  
 若要取得有關從 SQL Server 2005 升級的 PDF 格式資料工作表，請[按一下這裡](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf)（而不是下方的縮圖影像）。  
  
 ![有關從 SQL Server 2005 升級的資料工作表](../../../2014/sql-server/install/media/sqlserver2005eos.png "有關從 SQL Server 2005 升級的資料工作表")  
  
## <a name="choose-your-upgrade-option"></a>選擇升級選項  
 如果您要從 SQL Server 2005 升級關係資料庫，以下是 Microsoft 平臺上的關聯式儲存體選項。  
  
 若要查看這些選項更全面的分析，請 [按一下這裡](https://sql05upgrade.azurewebsites.net/)。  
  
|關聯式儲存體選項|優點|其他考量因素|  
|-------------------------------|--------------|-------------------------------|  
|**內部部署 SQL Server**<br /><br /> 此選項適用於任何種類 (從交易系統到資料倉儲) 的應用程式。<br /><br /> 如需詳細資訊，請參閱[SQL Server 2014](https://www.microsoft.com/EN-US/server-cloud/products/sql-server/)。|因為軟硬體皆由您所管理，所以您幾乎能自由操控各項功能與規模調整功能。<br /><br /> 如果您要從 SQL Server 2005 升級，這是最相似的環境。|因為您必須購買、維護及管理您所擁有的硬體與軟體，所以此選項的初期投資最高，管理時間也最長。|  
|**裝載于 Azure 虛擬機器上的 SQL Server**<br /><br /> 您若希望享有下列便利，可考慮此選項。<br />-遷移至託管環境的優點。<br />-對操作環境的控制。<br />-SQL Server 熟悉的功能集。<br /><br /> 如需詳細資訊，請參閱[Azure 上的 SQL Server 虛擬機器總覽](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)。<br /><br /> 如需移轉的相關資訊，請參閱 [將資料庫移轉至 Azure VM 上的 SQL Server](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/)。|您可以快速從虛擬機器的映像庫快速進行部署。<br /><br /> 您可以使用完整的 SQL Server 功能集。<br /><br /> 您可以節省在伺服器軟硬體上的投資。 您只需按每小時的使用量付費。|您必須設定及管理 SQL Server 與作業系統軟體。|  
|**Azure SQL Database 主控的資料庫服務**<br /><br /> 若您需要價格較低、維護工作較少的解決方案，可以考慮此選項。<br /><br /> 此選項特別適合不需要隨時保有相同容量的應用程式，或需要提供外部存取的應用程式。<br /><br /> 如需詳細資訊，請參閱[SQL Database](https://azure.microsoft.com/services/sql-database/)。<br /><br /> 如需有關遷移的詳細資訊，請參閱將[SQL Server 資料庫移轉至 Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/)。|您可以快速部署及相應增加。<br /><br /> 您只需按每小時的使用量付費。<br /><br /> 服務的費用不只有儲存體而已，還包括高可用性及自動化備份。|Azure SQL Database 所缺少的一些 SQL Server 功能並不適用於託管的雲端環境。 如需詳細資訊，請參閱 [Azure SQL Database Transact-SQL 資訊](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/)。<br /><br /> 相較於 SQL Server 的 524 PB，Azure SQL Database 的資料庫大小上限為 500 GB。|  
  
 對於某些資料及應用程式，您也可考慮使用非關聯式或 NoSQL 解決方案。  
  
|非關聯式解決方案|優點|  
|------------------------------|--------------|  
|**Azure DocumentDB**<br /><br /> 您的現代化應用程式、可調式應用程式、行動應用程式及 Web 應用程式若是使用 JSON 資料，並需要兼具主動式查詢及交易式資料處理的功能，可以考慮此選項。<br /><br /> 如需詳細資訊，請參閱 [DocumentDB](https://azure.microsoft.com/services/documentdb/)。|您的文件會編製索引，讓您可以使用熟悉的 SQL 語法加以查詢。<br /><br /> 資料庫無須設定結構描述。<br /><br /> 您無須重建索引，就可將屬性加入文件中。<br /><br /> 資料庫引擎內就能直接提供您 JSON 及 JavaScript 支援。<br /><br /> 除可獲得地理空間資料的原生支援之外，還可與其他 Azure 服務整合，包括 Azure 搜尋、HDInsight 及資料 Factory。<br /><br /> 專用的輸送量層級讓儲存體能有低延遲、高效能的表現。|  
|**Azure 表格儲存體**<br /><br /> 若您需要價格實惠的解決方案來儲存以 PB 計的半結構化資料，可以考慮此選項。<br /><br /> 如需詳細資訊，請參閱 [資料表儲存體](https://azure.microsoft.com/services/storage/tables/)。|您無須將資料下線，就能持續改進您的應用程式與資料表結構描述。<br /><br /> 您無須分區化您的資料集，就能相應增加規模。<br /><br /> 異地備援支援可將您的資料複寫到多個區域。|  
  
 若要依 Microsoft 上的指示下載報表「從 SQL Server 2005 移轉」(包含升級選項的更多詳細資料)，請 [按一下這裡](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) (而不是下方的縮圖影像)。  
  
 ![有關從 SQL Server 2005 移轉的報表](../../../2014/sql-server/install/media/sqlserver2005migratingdoc.png "有關從 SQL Server 2005 移轉的報表")  
  
## <a name="plan-your-upgrade"></a>規劃升級  
  
-   透過以下來自 SQL Server 小組的一系列部落格文章，了解如何計劃您的升級。  
  
    -   [從 SQL Server 2005 規劃有效率的升級：步驟1之3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [從 SQL Server 2005 規劃有效率的升級：步驟2之3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [從 SQL Server 2005 規劃有效率的升級：步驟3之3](https://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   請參閱[規劃 SQL Server 安裝](../../../2014/sql-server/install/planning-a-sql-server-installation.md)的需求和考慮，包括[安裝 SQL Server 2014 的硬體和軟體需求](hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   了解如何升級。  
  
    -   檢閱可用的升級方法，並了解 [升級 Database Engine](../../database-engine/install-windows/upgrade-database-engine.md)主題中的規劃方式與測試。  
  
        > [!IMPORTANT]  
        >  您無法將 SQL Server 2005 伺服器就地升級至 SQL Server 2014 伺服器。 您必須安裝 SQL Server 2014，然後將 SQL Server 2005 資料庫移轉到新的安裝。  
  
    -   若要取得詳細的 PDF 格式《技術升級指南》，請 [按一下這裡](https://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf)。  
  
-   如需詳細資訊、指引及取得工具以規劃及自動化您的升級或移轉，請參閱 [不再支援 SQL Server 2005](https://www.microsoft.com/server-cloud/products/sql-server-2005/)。  
  
## <a name="get-sql-server-2014"></a>取得 SQL Server 2014  
 若要下載 SQL Server 2014 的評估版，請[按一下這裡](https://www.microsoft.com/evalcenter/evaluate-sql-server-2014)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014](https://www.microsoft.com/server-cloud/products/sql-server/default.aspx)   
 [SQL Server 2005 結束支援](https://www.microsoft.com/server-cloud/products/sql-server-2005/)   
 [從 SQL Server 2005 升級到 SQL Server 2016](https://msdn.microsoft.com/library/mt168847.aspx)  
  
  
