---
title: SQL Server 2014 混合雲端簡介 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fccd4169245421dd33cb5f41bac85861679de823
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088615"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>SQL Server 2014 混合雲端簡介
 大多數應用程式都面臨一些重要挑戰，例如提高效率、商業價值、複雜的硬體組態、視需要的大規模尖峰時段以及符合業界和公司的法規。 考量所有的這些因素並建立企業等級的技術是一項非常具挑戰性的工作。 Microsoft 混合雲端策略提供了傳統、私人雲端、公用雲端和混合雲端環境的支援，可克服這些重大的挑戰。 
 
 當您的公司需要可視需要擴充的彈性 IT 基礎結構時，您可以建置您的資料中心中的私人雲端或公用雲端中 Azure 全球資料中心。 當您擴充資料中心使其符合公用雲端時，您就是在建立混合雲端模型。 
 
 本主題將介紹支援混合雲端案例的 SQL Server 2014 功能。 如需有關 Microsoft 混合雲端策略和 SQL Server 的詳細資訊，請參閱 [SQL Server 混合 IT](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) 網站。 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server、 Azure 和混合式雲端 
 利用 Microsoft 技術，您可以在內部部署環境和雲端中執行程式碼、使用內部部署資料在雲端中執行，或是完全在可利用多個資料中心的雲端中執行。 因此，您可以按自己的步調將應用程式轉移至雲端，同時保有現有舊式 IT 投資的價值。 
 
 在本文中，我們將焦點放在從內部部署 SQL Server 跨越到 Azure 公用雲端方案的混合式雲端案例：[Azure 虛擬機器中的 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)並[Azure 儲存體](http://www.azure.com/documentation/services/storage/)。 具體來說，我們將討論下列案例： 
 
-  [備份及還原資料庫至/從 Azure 儲存體](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Azure 虛擬機器上維護資料庫複本](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [將 SQL Server 資料檔案儲存在 Azure 儲存體](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [現有的 SQL Server 資料庫移轉至 Azure 虛擬機器](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>適用於 SQL Server 和 Microsoft Azure 的混合式雲端案例 
 
#### <a name="backup"></a> 備份及還原資料庫至/從 Azure 儲存體 
 其中一項最基本的管理員工作就是備份和還原資料庫。 使用 SQL Server 和 Azure，您可以安全地備份您在雲端中的資料庫。 
 
 使用 Azure 儲存體中的 SQL Server 的備份和還原功能，做為備份目的地的主要優點包括： 
 
-  沒有限制的低成本儲存體 
 
-  高可用性的儲存體 (可確保資料不會遺失的地理位置複寫) 
 
-  可支援災害復原和規範需求的異地儲存體 
 
-  簡化的遠端備份和還原程序 
 
 下列是雲端和內部部署案例適用的 SQL Server 備份和還原功能清單： 
 
-  [SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)功能可讓您備份至 Azure 儲存體所指定 URL 當做備份目的地。 有了這項功能，您可以執行手動備份或是設定自己的備份策略，就像對於本機儲存體或其他異地選項的處理方式一樣。 
 
-  [備份加密](../relational-databases/backup-restore/backup-encryption.md)功能可讓您建立儲存體目的地的備份時加密資料： 內部部署和 Azure 儲存體。 
 
-  [備份壓縮 (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md)功能可讓您建立的備份小於相同資料的未壓縮備份。 壓縮備份需要較少的裝置 I/O，因此通常會大幅提高備份速度。 Azure 儲存體中儲存備份檔案時，這可以顯示了絕佳權益。 
 
-  [SQL Server Managed Backup 到 Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx)功能可讓您將 SQL Server 資料庫自動備份到[Azure 儲存體](http://www.azure.com/documentation/services/storage/)。 有了這項功能，您可以設定由 SQL Server 管理單一資料庫或多個資料庫的備份策略與排程備份，或是在執行個體層級設定預設值。 
 
-  [SQL Server Backup to Azure 工具](https://www.microsoft.com/download/details.aspx?id=40740)可用來備份至 Azure Blob 儲存體，以及加密和壓縮儲存在本機或雲端中的 SQL Server 備份。 此工具會啟用橫跨數個 SQL Server 版本的單一雲端備份策略，例如 SQL Server 2005、2008、2008 R2 和 2014。 
 
#### <a name="replica"></a> Azure 虛擬機器上維護資料庫複本 
 穩定的災害復原解決方案，為您的資料庫都很重要，您的企業邁向成功。 大多數的客戶都需要設定災害復原網站及針對資料庫複本購買額外的硬體。 使用 SQL Server 和 Azure，您可以維護您的資料庫，在雲端中的一或多個複本。 
 
 Azure 中維護次要複本的主要優點包括： 
 
-  低成本的災害復原解決方案 
 
-  透明的應用程式容錯移轉 
 
-  可卸載讀取工作負載和備份的可用複本 
 
 您可以使用任何下列技術，以維持在 Azure 中的次要複本： 
 
-  [加入 Azure 複本精靈](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx)可讓您將資料庫的一或多個複本部署到 Azure 中的虛擬機器災害復原。 
 
-  AlwaysOn 可用性群組、 資料庫鏡像和記錄傳送是最常見的技術，可用來解決您的應用程式的高可用性和災害復原需求。 如需資訊，請參閱[高可用性和災害復原 Azure 虛擬機器中 SQL Server](https://msdn.microsoft.com/library/azure/jj870962.aspx)。 
 
#### <a name="store"></a> 將 SQL Server 資料檔案儲存在 Azure 儲存體 
 將內部部署 SQL Server 資料檔案儲存在 Azure 儲存體中的資料庫提供彈性、 可靠及無限制的異地儲存體。 從 SQL Server 2014 開始，您可以使用[Miceosoft Azure 中的 SQL Server 資料檔案](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure)將 SQL Server 資料庫檔案儲存在 Azure 儲存體。 使用此功能，您可以移動資料，並從內部部署資料庫記錄檔到 Azure 儲存體，同時保留內部部署上執行的 SQL Server 的計算節點。 這項功能可讓您擁有 Azure 儲存體中的無限制的儲存體容量。 
 
 將 SQL Server 資料檔案的 Azure 儲存體儲存的主要優點包括： 
 
-  無限制的低成本儲存體，在 Azure 儲存體 
 
-  最適合用來將歷程記錄讀取工作負載卸載到雲端，以支援內部部署報告應用程式 
 
-  您可藉由分隔運算執行個體 (SQL Server 執行個體) 與資料 (SQL Server 資料檔案) 來加速災害復原。 這可讓您輕鬆地將資料庫附加到另一個 SQL Server 執行個體的內部部署環境中，或發生災害時的 Azure 虛擬機器中。 
 
#### <a name="migrate"></a> 現有的 SQL Server 資料庫移轉至 Azure 虛擬機器 
 雲端運算為企業帶來一些重要的好處，例如，不受限制的虛擬化資源將會以按次計費方式提供給您使用，您可以利用公開可用的雲端資料中心，而不用自行建立及管理資料中心，因此可大幅降低 IT 和硬體成本。 
 
 具有[在 「 Azure 虛擬機器 」 中的 SQL Server](https://msdn.microsoft.com/library/azure/jj823132.aspx)，您可以將現有內部部署應用程式至 Azure 最少或沒有程式碼變更。 管理員和開發人員仍然可以使用在內部部署環境提供的相同開發和管理工具。 
 
 從內部部署 SQL Server 的資料庫移到 SQL Server 在 Azure 虛擬機器中執行通常會採用其中一個途徑： 
 
-  **只移動資料庫：** 有數個工具和技術可用來將現有的內部部署資料庫移到 Azure 虛擬機器中 SQL Server。 指導方針和移轉至 Azure 虛擬機器中 SQL Server 的建議，請參閱[準備移轉到 Azure 虛擬機器中 SQL Server](https://msdn.microsoft.com/library/dn133142.aspx)以及[移轉至 Azure 虛擬機器中的 SQL Server](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   此外，從 SQL Server 2014，新的精靈[將 SQL Server 資料庫部署到 Microsoft Azure 虛擬機器](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)可讓您將資料庫部署到 Azure 虛擬機器中執行的另一個 SQL Server 執行個體。 
 
-  **移動整部虛擬機器：** 您可以將您自己的 SQL Server 虛擬機器帶到 Azure，或使用平台映像建立一個。 然後，您可以將已經包含資料的資料磁碟上傳及附加到虛擬機器，或是將空的磁碟附加到機器。 需要 SQL Server 資料執行個體具有連結的資料磁碟的 Azure 虛擬機器上提供您的資料檔案和應用程式資料的另一個的永續性儲存體。 如需完整資訊和使用說明，請參閱[SQL Server 部署在 Azure 虛擬機器](https://msdn.microsoft.com/library/dn133141.aspx)。 
 
 如果您打算將應用程式層 （例如展示層、 商業層和資料庫層） 移至 Azure 虛擬機器，我們建議您檢閱中提供的建議[應用程式模式和開發在 「 Azure 虛擬機器 」 中的 SQL Server 的策略](https://msdn.microsoft.com/library/dn574746.aspx)文章。 本文的目的是提供解決方案架構設計人員和開發人員的基礎良好的應用程式架構和設計，他們可以遵循移轉至 Azure，以及開發新的應用程式在 Azure 中的現有應用程式時。 此文章會針對每個應用程式模式描述內部部署案例、其各自的雲端功能解決方案及相關的技術建議。 此外，本文還討論特定的 Azure 開發策略，以便您可以正確地設計您的應用程式。 
 
## <a name="see-also"></a>另請參閱 
 [SQL Server 2014 CTP2 產品指南](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Microsoft SQL Server 混合雲端部落格系列](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [將以資料為中心的應用程式移轉至 Azure](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
 
