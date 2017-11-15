---
title: "遠端 BLOB 存放區 (RBS) 及 AlwaysOn 可用性群組 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d17e70f0a9a14323c48943820afefbec9581547
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="remote-blob-store-rbs-and-always-on-availability-groups-sql-server"></a>遠端 BLOB 存放區 (RBS) 及 AlwaysOn 可用性群組 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可以為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][遠端 BLOB 存放區 (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) BLOB 物件 (Blob) 提供高可用性和災害復原方案。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 會透過將儲存在可用性資料庫中的任何 RBS 中繼資料和結構描述複寫到次要複本，予以保護。 這是 SharePoint 內容資料庫。 一般而言， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分開儲存此 RBS 中繼資料與 BLOB。  
  
 RBS BLOB 資料的保護取決於 BLOB 存放區位置，如下所示：  
  
|BLOB 存放區位置|可用性群組可保護此 BLOB 資料？|  
|-------------------------|-----------------------------------------------------|  
|包含 RBS 中繼資料的相同資料庫 (使用 RBS 遠端 FILESTREAM 提供者所儲存)|是|  
|在相同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的另一個資料庫 (使用 RBS 遠端 FILESTREAM 提供者所儲存)|是<br /><br /> 我們建議您在包含 RBS 中繼資料之資料庫的同一個可用性群組中放置此資料庫。|  
|在不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的另一個資料庫 (使用 RBS 遠端 FILESTREAM 提供者所儲存)|是<br /><br /> 此資料庫必須位於個別的可用性群組。|  
|協力廠商 BLOB 存放區|否<br /><br /> 為了保護此 BLOB 資料，請使用 BLOB 存放區提供者的高可用性機制。|  
  
##  <a name="Limitations"></a> 限制  
  
-   RBS 維護程式在主要複本上需要為目標。  
  
##  <a name="Recommendations"></a> 建議  
  
-   使用可用性群組接聽程式。 如需詳細資訊，請參閱 [可用性群組接聽程式、用戶端連接及應用程式容錯移轉 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)中心概念。  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [維護遠端 BLOB 存放區](http://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) (在《 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 線上叢書》中)  
  
-   [執行 RBS 維護程式](http://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (部落格)  
  
-   [使用 FILESTREAM 提供者設定遠端 BLOB 儲存 (RBS) (SharePoint 2010)](http://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (部落格)  
  
## <a name="see-also"></a>另請參閱  
 [一律開啟用戶端連接性 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [遠端 Blob 存放區 &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
