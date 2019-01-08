---
title: AlwaysOn 可用性群組：互通性 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3f6123f66d687327ba56601419328e44fd920a2a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367994"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>AlwaysOn 可用性群組：互通性 (SQL Server)
  本主題記錄 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中其他 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]功能的互通性。  
  

  
##  <a name="Interop"></a> 與 AlwaysOn 可用性群組互通的功能  
 下表列出與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 互通的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]功能。 **[詳細資訊]** 資料行中的連結表示有適用於所指功能的互通性考量。  
  
|功能|[詳細資訊]|  
|-------------|----------------------|  
|異動資料擷取|[複寫、 變更追蹤、 異動資料擷取和 AlwaysOn 可用性群組&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|變更追蹤|[複寫、 變更追蹤、 異動資料擷取和 AlwaysOn 可用性群組&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|自主資料庫|[自主的資料庫與 AlwaysOn 可用性群組 (SQL Server)](always-on-availability-groups-sql-server.md)|  
|資料庫加密|[加密的資料庫與 AlwaysOn 可用性群組&#40;SQL Server&#41;](encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|資料庫快照集|[資料庫快照集與 AlwaysOn 可用性群組&#40;SQL Server&#41;](database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM 與 FileTable|[FILESTREAM 和 FileTable 與 AlwaysOn 可用性群組&#40;SQL Server&#41;](filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|全文檢索搜尋|注意：全文檢索索引與 AlwaysOn 次要資料庫同步。|  
|記錄傳送|[從移轉的必要條件是記錄傳送至 AlwaysOn 可用性群組&#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|遠端 Blob 存放區 (RBS)|[遠端 Blob 存放區&#40;RBS&#41;和 AlwaysOn 可用性群組&#40;SQL Server&#41;](remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|複寫[設定 AlwaysOn 可用性群組 (SQL Server) 的複寫](configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [維護 AlwaysOn 發行集資料庫&#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [複寫、 變更追蹤、 異動資料擷取和 AlwaysOn 可用性群組&#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [複寫訂閱者及 AlwaysOn 可用性群組&#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Analysis Services 與 AlwaysOn 可用性群組](analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|利用唯讀次要複本做為報表資料來源，減少主要讀寫複本上的負載。<br /><br /> [Reporting Services 與 AlwaysOn 可用性群組&#40;SQL Server&#41;](reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Service Broker|[Service Broker 與 AlwaysOn 可用性群組&#40;SQL Server&#41;](service-broker-with-always-on-availability-groups-sql-server.md)|  
|SQL Server Agent||  
  
##  <a name="NoInterop"></a> 不與 AlwaysOn 可用性群組互通的功能  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 無法與下列功能互通：  
  
-   跨資料庫交易/分散式交易  
  
     如需這類交易不受支援之原因的相關資訊，請參閱[資料庫鏡像或 AlwaysOn 可用性群組不支援跨資料庫交易 &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md)。  
  
-   資料庫鏡像  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [移轉指南：移轉至 SQL Server 2012 容錯移轉叢集和可用性群組從先前叢集和鏡像部署](https://blogs.msdn.com/b/sqlalwayson/archive/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments.aspx)  
  
     [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮書：**  
  
     [移轉指南：移轉至 AlwaysOn 可用性群組從先前的部署結合資料庫鏡像與記錄傳送](https://msdn.microsoft.com/library/jj635217)  
  
     [Microsoft SQL Server AlwaysOn 解決方案指南高可用性和災害復原](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft 的 SQL Server 2012 白皮書](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客戶諮詢團隊白皮書](http://sqlcat.com/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [必要條件、 限制和建議，AlwaysOn 可用性群組的&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
