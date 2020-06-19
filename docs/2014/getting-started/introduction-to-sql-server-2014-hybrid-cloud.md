---
title: SQL Server 2014 混合式雲端簡介 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 93282199db986ab8bcf18b05f9ae8b61a5a45b9a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926739"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>SQL Server 2014 混合雲端簡介
 大多數應用程式都面臨一些重要挑戰，例如提高效率、商業價值、複雜的硬體組態、視需要的大規模尖峰時段以及符合業界和公司的法規。 考量所有的這些因素並建立企業等級的技術是一項非常具挑戰性的工作。 Microsoft 混合雲端策略提供了傳統、私人雲端、公用雲端和混合雲端環境的支援，可克服這些重大的挑戰。 
 
 當您的企業需要可隨需調整的彈性 IT 基礎結構時，您可以在資料中心或 Azure 全球資料中心內的公用雲端中建立私人雲端。 當您擴充資料中心使其符合公用雲端時，您就是在建立混合雲端模型。 
 
 本主題將介紹支援混合雲端案例的 SQL Server 2014 功能。 如需有關 Microsoft 混合雲端策略和 SQL Server 的詳細資訊，請參閱 [SQL Server 混合 IT](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) 網站。 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server、Azure 和混合式雲端 
 利用 Microsoft 技術，您可以在內部部署環境和雲端中執行程式碼、使用內部部署資料在雲端中執行，或是完全在可利用多個資料中心的雲端中執行。 因此，您可以按自己的步調將應用程式轉移至雲端，同時保有現有舊式 IT 投資的價值。 
 
 在本文中，我們會將焦點放在從內部部署 SQL Server 到 Azure 公用雲端供應專案的混合式雲端案例： [azure 虛擬機器](https://msdn.microsoft.com/library/azure/jj823132.aspx)和[Azure 儲存體](https://www.azure.com/documentation/services/storage/)中的 SQL Server。 具體而言，我們將討論下列案例： 
 
-  [Azure 儲存體備份和還原資料庫](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [維護 Azure 虛擬機器上的資料庫複本](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [將 SQL Server 的資料檔案儲存在 Azure 儲存體](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [將現有 SQL Server 資料庫移轉至 Azure 虛擬機器](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>SQL Server 和 Microsoft Azure 的混合式雲端案例 
 
#### <a name="backup-and-restore-databases-tofrom-azure-storage"></a><a name="backup"></a>Azure 儲存體備份和還原資料庫 
 其中一項最基本的管理員工作就是備份和還原資料庫。 有了 SQL Server 和 Azure，您就可以在雲端中安全地備份您的資料庫。 
 
 使用 SQL Server 的備份與還原功能搭配 Azure 儲存體作為備份目的地的主要優點包括： 
 
-  沒有限制的低成本儲存體 
 
-  高可用性的儲存體 (可確保資料不會遺失的地理位置複寫) 
 
-  可支援災害復原和合規性需求的異地儲存體 
 
-  簡化的遠端備份和還原程序 
 
 下列是雲端和內部部署案例適用的 SQL Server 備份和還原功能清單： 
 
-  [SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) ] 功能可讓您藉由指定 URL 做為備份目的地，來備份至 Azure 儲存體。 有了這項功能，您可以執行手動備份或是設定自己的備份策略，就像對於本機儲存體或其他異地選項的處理方式一樣。 
 
-  [備份加密](../relational-databases/backup-restore/backup-encryption.md)功能可讓您在為儲存目的地建立備份時加密資料：內部部署和 Azure 儲存體。 
 
-  [[備份壓縮（SQL Server）](../relational-databases/backup-restore/backup-compression-sql-server.md) ] 功能可讓您建立備份，其小於相同資料的未壓縮備份。 壓縮備份需要較少的裝置 I/O，因此通常會大幅提高備份速度。 在 Azure 儲存體中儲存備份檔案時，這可以帶來絕佳的優勢。 
 
-  [SQL Server 受控備份至 Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) ] 功能可讓您將 SQL Server 資料庫自動備份至[Azure 儲存體](https://www.azure.com/documentation/services/storage/)。 有了這項功能，您可以設定由 SQL Server 管理單一資料庫或多個資料庫的備份策略與排程備份，或是在執行個體層級設定預設值。 
 
-  [SQL Server 備份至 Azure 工具](https://www.microsoft.com/download/details.aspx?id=40740)可讓備份 Azure Blob 儲存體，並加密和壓縮儲存在本機或雲端中的 SQL Server 備份。 此工具會啟用橫跨數個 SQL Server 版本的單一雲端備份策略，例如 SQL Server 2005、2008、2008 R2 和 2014。 
 
#### <a name="maintain-database-replicas-on-azure-virtual-machines"></a><a name="replica"></a>維護 Azure 虛擬機器上的資料庫複本 
 針對您的資料庫擁有穩定的嚴重損壞修復解決方案，對於您的企業成功來說是不可或缺的。 大多數的客戶都需要設定災害復原網站及針對資料庫複本購買額外的硬體。 透過 SQL Server 和 Azure，您可以在雲端中維護資料庫的一個或多個複本。 
 
 在 Azure 中維護次要複本的主要優點包括： 
 
-  低成本的災害復原解決方案 
 
-  透明的應用程式容錯移轉 
 
-  可卸載讀取工作負載和備份的可用複本 
 
 您可以使用下列任何一種方法，在 Azure 中維護次要複本： 
 
-  [[加入 Azure 複本] 嚮導](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx)可讓您將資料庫的一個或多個複本部署到 Azure 中的虛擬機器，以進行嚴重損壞修復。 
 
-  AlwaysOn 可用性群組、資料庫鏡像和記錄傳送都是最常見的技術，可讓您用來解決應用程式的高可用性和嚴重損壞修復需求。 如需詳細資訊，請參閱[Azure 虛擬機器中 SQL Server 的高可用性和嚴重損壞修復](https://msdn.microsoft.com/library/azure/jj870962.aspx)。 
 
#### <a name="store-sql-server-data-files-in-azure-storage"></a><a name="store"></a>將 SQL Server 的資料檔案儲存在 Azure 儲存體 
 將內部部署 SQL Server 資料檔案儲存在 Azure 儲存體為您的資料庫提供彈性、可靠且無限制的離站儲存體。 從 SQL Server 2014 開始，您可以[在 Miceosoft Azure 中使用 SQL Server 的資料檔案](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure)，在 Azure 儲存體中儲存 SQL Server 資料庫檔案。 透過這項功能，您可以將資料和記錄檔從內部部署資料庫移至 Azure 儲存體，同時將 SQL Server 的計算節點保留在內部部署環境中執行。 這項功能可讓您在 Azure 儲存體中擁有不受限制的儲存容量。 
 
 儲存 SQL Server 資料檔案的主要優點 Azure 儲存體包括： 
 
-  Azure 儲存體中無限制的低成本儲存體 
 
-  最適合用來將歷程記錄讀取工作負載卸載到雲端，以支援內部部署報告應用程式 
 
-  您可藉由分隔運算執行個體 (SQL Server 執行個體) 與資料 (SQL Server 資料檔案) 來加速災害復原。 這可讓您輕鬆地將資料庫附加到內部部署環境中的另一個 SQL Server 實例，或在發生嚴重損壞時于 Azure 虛擬機器中。 
 
#### <a name="migrate-existing-sql-server-databases-to-azure-virtual-machines"></a><a name="migrate"></a>將現有 SQL Server 資料庫移轉至 Azure 虛擬機器 
 雲端運算為企業帶來一些重要的好處，例如，不受限制的虛擬化資源將會以按次計費方式提供給您使用，您可以利用公開可用的雲端資料中心，而不用自行建立及管理資料中心，因此可大幅降低 IT 和硬體成本。 
 
 使用[Azure 虛擬機器中的 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)，您可以將現有的內部部署應用程式移至 azure，只需變更程式碼即可。 管理員和開發人員仍然可以使用在內部部署環境提供的相同開發和管理工具。 
 
 將資料庫從內部部署 SQL Server 移至 Azure 虛擬機器中執行的 SQL Server 通常會採用下列其中一個路徑： 
 
-  **只移動資料庫：** 有數種工具和技術可用來將現有的內部部署資料庫移至 Azure 虛擬機器中的 SQL Server。 如需在 Azure 虛擬機器中遷移至 SQL Server 的指導方針和建議，請參閱[準備在 azure 虛擬機器中遷移至 SQL Server](https://msdn.microsoft.com/library/dn133142.aspx)並同時[遷移至 azure 虛擬機器中的 SQL Server](https://msdn.microsoft.com/library/jj156165.aspx)。 
 
   此外，從 SQL Server 2014 開始，您可以使用新的 wizard 將[SQL Server 資料庫部署到 Microsoft Azure 的虛擬機器](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)，將資料庫部署到 Azure 虛擬機器中執行的另一個 SQL Server 實例。 
 
-  **移動整個虛擬機器：** 您可以將自己的 SQL Server 虛擬機器帶入 Azure，或使用平臺映射來建立一個。 然後，您可以將已經包含資料的資料磁碟上傳及附加到虛擬機器，或是將空的磁碟附加到機器。 在 Azure 虛擬機器上使用已連接資料磁片的 SQL Server 資料實例，可為您的資料檔案和應用程式資料提供另一個持續性儲存體。 如需完整資訊和操作說明，請參閱[Azure 虛擬機器中的 SQL Server 部署](https://msdn.microsoft.com/library/dn133141.aspx)。 
 
 如果您打算將應用層（例如展示層、商業層和資料庫層）移至 Azure 虛擬機器，建議您參閱[azure 虛擬機器文章中 SQL Server 的應用程式模式和開發策略](https://msdn.microsoft.com/library/dn574746.aspx)中提供的建議。 本文的目的在於為解決方案架構師和開發人員提供基礎良好的應用程式架構和設計，讓他們將現有應用程式移轉至 Azure，以及在 Azure 中開發新應用程式時可以採用。 此文章會針對每個應用程式模式描述內部部署案例、其各自的雲端功能解決方案及相關的技術建議。 此外，本文還討論特定的 Azure 開發策略，讓您可以正確地設計應用程式。 
 
## <a name="see-also"></a>另請參閱 
 [SQL Server 2014 CTP2 產品指南](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Microsoft SQL Server 混合雲端部落格系列](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [將以資料為中心的應用程式遷移至 Azure](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
