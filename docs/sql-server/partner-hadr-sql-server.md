---
title: SQL Server 高可用性和災害復原夥伴
description: 具有 Server 監視解決方案的協力廠商夥伴清單。
ms.topic: conceptual
ms.custom: seo-dt-2019
ms.date: 09/17/2017
ms.prod: sql
ms.technology: release-landing
ms.author: mikeray
author: MikeRayMSFT
ms.openlocfilehash: 5fd19ca04a383ca8485d2668a7988c8558040f76
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923044"
---
# <a name="sql-server-high-availability-and-disaster-recovery-partners"></a>SQL Server 高可用性和災害復原夥伴
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
若要為您的 SQL Server 服務提供高可用性和災害復原，您可以從各種領先業界的工具中選擇。  本文章特別介紹提供 Microsoft SQL Server 高可用性和災害復原解決方案支援的 Microsoft 夥伴公司。

## <a name="high-availability-and-disaster-recovery-partners"></a>高可用性和災害復原夥伴

| Partner | 描述 | 連結 | 
| --- | --- | --- |
|![Azure][5] |**Azure Site Recovery**<br>Site Recovery 會複寫在虛擬機器或實體伺服器上執行的工作負載，讓這些工作負載無法在主要站台使用時，仍可在次要位置使用。 您可以將 SQL Server 虛擬機器從內部部署資料中心複寫及容錯移轉到 Azure 或其他內部部署資料中心，或從一個 Azure 資料中心複寫及容錯移轉到另一個 Azure 資料中心。<br><br> Enterprise 和 Standard 版的 SQL Server 2008 R2 - SQL Server 2016|[網站][azure_website]<br>[Marketplace][azure_marketplace] \(英文\)<br>[資料工作表][azure_datasheet]<br>[Twitter][azure_twitter]<br>[影片][azure_youtube]|
|![DH2i][2] |**DH2i**<br>DxEnterprise 是適用於 Windows、Linux 和 Docker 的智慧型可用性軟體，有助於您幾乎完全避免規劃和未規劃的停機、節省大量成本、大幅簡化管理，並讓您兼具實體和邏輯彙總。<br><br>SQL Server 2005+、Windows Server 2008R2+、Ubuntu 16+、RHEL 7+、CentOS 7+|[網站][dh2i_website]<br>[資料工作表][dh2i_datasheet]<br>[Twitter][dh2i_twitter]<br>[影片][dh2i_youtube]|
|![HPE][4] |**HPE Serviceguard**<br>使用 HPE Serviceguard for Linux (SGLX)，可在任何距離的實體和虛擬環境之間發現大量基礎結構和應用程式錯誤，以防止 Linux &reg; 上的重要 SQL Server 2017 工作負載發生規劃和未規劃停機。 針對容錯移轉叢集執行個體和 AlwaysOn 可用性群組 SQL Server 工作負載，HPE SGLX A.12.20.00 和更新版本提供內容相關性監視和復原選項。 HPE SGLX 讓運作時間最大化，同時仍顧及資料完整性和效能。<br><br>Linux 上的 SQL Server 2017 - RedHat 7.3、7.4、SUSE 12 SP2、SP3|[網站][hpe_website]<br>[資料工作表][hpe]<br>[下載評估][hpe_download]<br>[部落格][hpe_download]<br>[Twitter][hpe_twitter]
|![IDERA][3]|**IDERA**<br>SQL Safe Backup 是適用於 SQL Server 的高效能備份和復原解決方案，透過減少資料庫備份的時間和備份檔案大小，以及提供備份檔案內資料庫的立即讀取和立即寫入存取權，來省下大筆費用。<br><br>Microsoft SQL Server：2005 SP1 或更新版、2008、2008 R2、2012、2014、2016；所有版本 |[網站][idera_website]|
|![NEC][7]|**NEC**<br>ExpressCluster 是全方位且完全自動化的高可用性和災害復原解決方案，可處理所有主要失敗，包括在實體電腦上或在內部部署或雲端環境中虛擬機器上執行之 SQL Server 和相關應用程式的硬體、軟體、網路和站台失敗。<br><br>Microsoft SQL Server：2005 或更新版；所有版本 |[網站][necec_website]<br>[資料工作表][necec_datasheet]<br>[影片][necec_youtube]<br>[下載][necec_download]|
|![Portworx][6] |**Portworx**<br>Portworx 是在生產環境中執行之具狀態容器的解決方案。 Portworx 可讓使用者使用任何容器排程器 (包括 Kubernetes、Mesosphere DC/OS 和 Docker Swarm)，在任何基礎結構上管理任何資料庫或具狀態服務。 Portworx 解決了 DevOps 小組在生產環境中執行容器化資料庫和其他具狀態服務時最常遇到的五個問題：持續性、高可用性、資料自動化、多個資料存放區和基礎結構的支援，以及安全性。<br><br>Docker 上的 SQL Server 2017 |[網站][portworx_website]<br>[文件集][portworx_docs]<br>[影片][portworx_youtube]|
|![SIOS][8] |**SIOS**<br>SIOS Technology 針對 Windows 或 Linux 版 SQL Server 提供具成本效益的高可用性和災害復原解決方案。 SIOS SANless 叢集可降低對共用存放裝置 SAN 的需求，讓您有完整的彈性可保護您位於實體環境、虛擬環境、雲端與混合式雲端組態 (不論這些環境位於單一站台或多站台) 中最重要的應用程式。<br><br>新增 SIOS DataKeeper 到您的 Windows Server 容錯移轉叢集環境以建立無 SAN 的磁碟區資源，取代傳統共用存放裝置，可讓您輕鬆地在 Azure 中執行 WSFC。<br><br>SIOS Protection Suite 是具有高度彈性的叢集解決方案，它可以保護關鍵 Linux 應用程式，例如 SQL Server、SAP、HANA、Oracle 與許多其他項目。|[網站][sios_website]<br>[資料工作表][sios_datasheet]<br>[Twitter][sios_twitter]<br>[Marketplace][sios_marketplace] \(英文\)<br>[影片][sios_youtube]|
|![Veeam][1] |**Veeam**<br>Veeam Backup & Replication 是功能強大、容易使用且經濟實惠的備份和可用性解決方案。 它提供快速、彈性又可靠的虛擬化應用程式和資料復原功能，將 VM (虛擬機器) 備份及複寫結合在單一軟體解決方案中。 Veeam Backup & Replication 提供獲獎肯定的 VMware vSphere 和 Microsoft Hyper-V 虛擬環境支援。<br><br>Windows 上的 SQL Server 2005 SP4-SQL Server 2016 |[網站][veeam_website]<br>[資料工作表][veeam_datasheet]<br>[Twitter][veeam_twitter]<br>[影片][veeam_youtube]|

## <a name="next-steps"></a>後續步驟
若要深入了解其他合作夥伴，請參閱[監視][mon_partners]、[管理合作夥伴][management_partners]及[開發合作夥伴][dev_partners]。

<!--Image references-->
[1]: ./media/partner-hadr-sql-server/Veeam-green-logo.png
[2]: ./media/partner-hadr-sql-server/dh2i-logo.png
[3]: ./media/partner-hadr-sql-server/idera-logo.png
[4]: ./media/partner-hadr-sql-server/hpe.png
[5]: ./media/partner-hadr-sql-server/azure-logo.png
[6]: ./media/partner-hadr-sql-server/portworx-logo.png
[7]: ./media/partner-hadr-sql-server/nec-logo.png
[8]: ./media/partner-hadr-sql-server/sios-logo.png

<!--Article links-->
[mon_partners]: ./partner-monitor-sql-server.md
[management_partners]: ./partner-management-sql-server.md
[dev_partners]: ./partner-dev-sql-server.md

<!--Website links -->
[veeam_website]:https://www.veeam.com/
[dh2i_website]:https://dh2i.com
[idera_website]:https://www.idera.com/productssolutions/sqlserver
[hpe_website]: https://www.hpe.com/us/en/product-catalog/detail/pip.376220.html
[azure_website]: https://docs.microsoft.com/azure/site-recovery/site-recovery-sql
[necec_website]: https://www.necam.com/ExpressCluster/
[portworx_website]: https://portworx.com/
[sios_website]: https://us.sios.com/

<!--Get Started Links-->

<!--Datasheet Links-->
[veeam_datasheet]:https://www.veeam.com/veeam_backup_9_5_datasheet_en_ds.pdf
[dh2i_datasheet]:https://dh2i.com/wp-content/uploads/DxE-Win-QuickFacts.pdf
[hpe]:https://www.hpe.com/h20195/v2/default.aspx?cc=us&lc=en&oid=376220
[necec_datasheet]: https://www.necam.com/docs/?id=0d9ef7a7-f935-4909-b6bb-20a47b3
[azure_datasheet]: /azure/site-recovery/vmware-physical-azure-support-matrix
[sios_datasheet]: https://us.sios.com/solutions/high-availability-cluster-software-cloud/

<!--Marketplace Links -->
[azure_marketplace]: https://azuremarketplace.microsoft.com/marketplace/apps?search=site%20recovery&page=1
[sios_marketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/sios_datakeeper.sios-datakeeper-8
<!--Press links-->
<!--[veeam_press]:-->

<!--YouTube links-->
[veeam_youtube]:https://www.youtube.com/user/YouVeeam
[dh2i_youtube]:https://www.youtube.com/user/dh2icompany 
[idera_youtube]:https://www.idera.com/resourcecentral/videos/sql-safe-overview
[azure_youtube]: https://mva.microsoft.com/en-US/training-courses/is-your-lack-of-a-disaster-recovery-site-keeping-you-up-at-night-8680?l=oF7YrFH1_7504984382
[necec_youtube]: https://www.youtube.com/watch?v=9La3Cw1Q1Jk
[portworx_youtube]: https://www.youtube.com/channel/UCSexpvQ9esSRgiS_Q9_3mLQ
[sios_youtube]: https://www.youtube.com/watch?v=U3M44gJNWQE

<!--Twitter links-->
[veeam_twitter]:https://twitter.com/veeam
[dh2i_twitter]:https://twitter.com/dh2i
[hpe_twitter]:https://twitter.com/hpe
[azure_twitter]:https://twitter.com/hashtag/azuresiterecovery
[sios_twitter]:https://www.twitter.com/SIOSTech

<!--Docs links>-->
[portworx_docs]: https://docs.portworx.com/

<!--Download links-->
[hpe_download]: https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=SGLX-DEMO
[necec_download]: https://www.necam.com/ExpressCluster/30daytrial/
<!--Blog links-->
[hpe_blog]: https://community.hpe.com/t5/Servers-The-Right-Compute/SQL-Server-for-Linux-Is-Here-and-A-New-Chapter-for-Mission/ba-p/6977571#.WiHWW0xFwUE
