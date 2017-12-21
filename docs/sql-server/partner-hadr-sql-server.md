---
title: "SQL Server 高可用性和災害復原夥伴 | Microsoft Docs"
description: "具有 Server 監視解決方案的協力廠商夥伴清單。"
services: sql-server
documentationcenter: NA
author: MikeRayMSFT
manager: jhubbard
editor: 
ms.assetid: 
ms.service: 
ms.component: sql-non-specified
ms.suite: sql
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-server
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.author: mikeray
ms.openlocfilehash: a37ba047d17dda983d3fbed247df38ebb3a1aaf8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-high-availability-and-disaster-recovery-partners"></a>SQL Server 高可用性和災害復原夥伴
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 若要為您的 SQL Server 服務提供高可用性和災害復原，您可以從各種領先業界的工具中選擇。  本文章特別介紹提供 Microsoft SQL Server 高可用性和災害復原解決方案支援的 Microsoft 夥伴公司。

## <a name="our-high-availability-and-disaster-recovery-partners"></a>我們的高可用性和災害復原夥伴
<!--|![PartnerShortName][1] |**PartnerShortName**<br>PartnerShortName Brief description of the type of products that partner provides. <br><br>List of supported versions of SQL Server, OS, OS platforms/distros  Server 2005 SP4 – SQL Server 2016 on Windows |[Datasheet][PartnerShortName_datasheet]<br>[Marketplace][PartnerShortName_marketplace]<br>[Website][PartnerShortName_website]<br>[Twitter][PartnerShortName_twitter]<br>[Video][PartnerShortName_youtube]|[![veem_video](./media/partner-hadr-sql-server/PartnerShortName_video.png)](https://www.youtube.com/channel/**************)
-->

| Partner | Description | 連結 | 
| --- | --- | --- |
|![azure][5] |**Azure Site Recovery**<br>Site Recovery 會複寫在虛擬機器或實體伺服器上執行的工作負載，讓這些工作負載無法在主要站台使用時，仍可在次要位置使用。 您可以將 SQL Server 虛擬機器從內部部署資料中心複寫及容錯移轉到 Azure 或其他內部部署資料中心，或從一個 Azure 資料中心複寫及容錯移轉到另一個 Azure 資料中心。<br><br> Enterprise 和 Standard 版的 SQL Server 2008 R2 - SQL Server 2016|[網站][azure_website]<br>[Marketplace][azure_marketplace]<br>[資料工作表][azure_datasheet]<br>[Twitter][azure_twitter]<br>[影片][azure_youtube]|
|![dh2i][2] |**DH2i**<br>DxEnterprise 是適用於 Windows、Linux 和 Docker 的智慧型可用性軟體，有助於您幾乎完全避免規劃和未規劃的停機、節省大量成本、大幅簡化管理，並讓您兼具實體和邏輯彙總。<br><br>SQL Server 2005+、Windows Server 2008R2+、Ubuntu 16+、RHEL 7+、CentOS 7+|[網站][dh2i_website]<br>[資料工作表][dh2i_datasheet]<br>[Twitter][dh2i_twitter]<br>[影片][dh2i_youtube]|
|![hpe][4] |**HPE Serviceguard**<br>使用 HPE Serviceguard for Linux (SGLX)，可在不同距離的實體和虛擬環境間發現大量的基礎結構和應用程式錯誤，以防止在 Linux ® 上重要的 SQL Server 2017 工作負載發生規劃和未規劃的停機。 HPE SGLX 是 Beta 程式的一部分，會針對容錯移轉叢集執行個體和 Always On 可用性群組 SQL Server 工作負載，提供內容相關性監視和復原選項。 HPE SGLX 讓運作時間最大化，同時仍顧及資料完整性和效能。<br><br>Linux 上的 SQL Server 2017 - RedHat 7.3、7.4、SUSE 12 SP2、SP3|[網站][hpe_website]<br>[資料工作表][hpe]<br>[下載 Beta][hpe_download]<br>[部落格][hpe_download]<br>[Twitter][hpe_twitter]
|![idera][3]|**IDERA**<br>SQL Safe Backup 是適用於 SQL Server 的高效能備份和復原解決方案，透過減少資料庫備份的時間和備份檔案大小，以及提供備份檔案內資料庫的立即讀取和立即寫入存取權，來省下大筆費用。<br><br>Microsoft SQL Server：2005 SP1 或更新版、2008、2008 R2、2012、2014、2016；所有版本 |[網站][idera_website]|
|![portworx][6] |**Portworx**<br>Portworx 是在生產環境中執行之具狀態容器的解決方案。 Portworx 可讓使用者使用任何容器排程器 (包括 Kubernetes、Mesosphere DC/OS 和 Docker Swarm)，在任何基礎結構上管理任何資料庫或具狀態服務。 Portworx 解決了 DevOps 小組在生產環境中執行容器化資料庫和其他具狀態服務時最常遇到的五個問題：持續性、高可用性、資料自動化、多個資料存放區和基礎結構的支援，以及安全性。<br><br>Docker 上的 SQL Server 2017 |[網站][portworx_website]<br>[文件集][portworx_docs]<br>[影片][portworx_youtube]|
|![veeam][1] |**Veeam**<br>Veeam Backup & Replication 是功能強大、簡單好用且經濟實惠的備份和可用性解決方案。 其提供快速、彈性又可靠的虛擬化應用程式和資料復原，將 VM (虛擬機器) 備份及複寫結合在單一軟體解決方案中。 Veeam Backup & Replication 提供獲獎肯定的 VMware vSphere 和 Microsoft Hyper-V 虛擬環境支援。<br><br>SQL Server 2005 SP4 – Windows 上的 SQL Server 2016 |[網站][veeam_website]<br>[資料工作表][veeam_datasheet]<br>[Twitter][veeam_twitter]<br>[影片][veeam_youtube]|



## <a name="next-steps"></a>後續的步驟
若要深入了解我們的其他合作夥伴，請參閱[監視][mon_partners]、[管理夥伴][management_partners]及[開發夥伴][dev_partners]。

<!--Image references-->
[1]: ./media/partner-hadr-sql-server/Veeam_green_logo.png
[2]: ./media/partner-hadr-sql-server/dh2i_logo.png
[3]: ./media/partner-hadr-sql-server/idera_logo.png
[4]: ./media/partner-hadr-sql-server/hpe_pri_grn_pos_rgb.png
[5]: ./media/partner-hadr-sql-server/azure_logo.png
[6]: ./media/partner-hadr-sql-server/portworx_logo.png

<!--Article links-->
[mon_partners]: ./partner-monitor-sql-server.md
[management_partners]: ./partner-management-sql-server.md
[dev_partners]: ./partner-dev-sql-server.md

<!--Website links -->
[veeam_website]:https://www.veeam.com/
[dh2i_website]:http://dh2i.com
[idera_website]:https://www.idera.com/productssolutions/sqlserver
[hpe_website]: https://www.hpe.com/us/en/product-catalog/detail/pip.376220.html
[azure_website]: http://docs.microsoft.com/azure/site-recovery/site-recovery-sql
[portworx_website]: https://portworx.com/

<!--Get Started Links-->

<!--Datasheet Links-->
[veeam_datasheet]:https://www.veeam.com/veeam_backup_9_5_datasheet_en_ds.pdf
[dh2i_datasheet]:http://dh2i.com/wp-content/uploads/DxE-Win-QuickFacts.pdf
[hpe]:https://www.hpe.com/h20195/v2/default.aspx?cc=us&lc=en&oid=376220
[azure_datasheet]: http://docs.microsoft.com/azure/site-recovery/site-recovery-sql#site-recovery-support

<!--Marketplace Links -->
[azure_marketplace]: https://azuremarketplace.microsoft.com/marketplace/apps?search=site%20recovery&page=1
<!--Press links-->
<!--[veeam_press]:-->

<!--YouTube links-->
[veeam_youtube]:https://www.youtube.com/user/YouVeeam
[dh2i_youtube]:https://www.youtube.com/user/dh2icompany 
[idera_youtube]:https://www.idera.com/resourcecentral/videos/sql-safe-overview
[azure_youtube]: https://mva.microsoft.com/en-US/training-courses/is-your-lack-of-a-disaster-recovery-site-keeping-you-up-at-night-8680?l=oF7YrFH1_7504984382
[portworx_youtube]: https://www.youtube.com/channel/UCSexpvQ9esSRgiS_Q9_3mLQ 

<!--Twitter links-->
[veeam_twitter]:https://twitter.com/veeam
[dh2i_twitter]:https://twitter.com/dh2i
[hpe_twitter]:https://twitter.com/hpe
[azure_twitter]: https://twitter.com/hashtag/azuresiterecovery

<!--Docs links>-->
[portworx_docs]: http://docs.portworx.com/

<!--Download links-->
[hpe_download]: http://downloads.linux.hpe.com/SDR/project/sglx/sglx-beta/

<!--Blog links-->
[hpe_blog]: https://community.hpe.com/t5/Servers-The-Right-Compute/SQL-Server-for-Linux-Is-Here-and-A-New-Chapter-for-Mission/ba-p/6977571#.WiHWW0xFwUE
