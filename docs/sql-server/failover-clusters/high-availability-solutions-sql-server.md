---
title: 高可用性方案 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
caps.latest.revision: 84
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 95b466c9740f42de3c0b7716a4e0c015133ee31f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="high-availability-solutions-sql-server"></a>高可用性解決方案 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題會介紹幾個可增進伺服器或資料庫可用性的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高可用性解決方案。 高可用性解決方案可遮蔽硬體或軟體失敗所造成的影響，並維護應用程式的可用性，進而讓使用者的停機時間減至最少。    
    
   
>  **注意！** 想要知道哪些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援指定的高可用性方案嗎？ 請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)的＜高可用性 (AlwaysOn)＞一節。    
     
    
##  <a name="TermsAndDefinitions"></a> SQL Server 高可用性解決方案概觀    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供幾個選項用於建立伺服器或資料庫的高可用性。 高可用性選項包括下列各項：    
    
*  AlwaysOn 容錯移轉叢集執行個體    
 AlwaysOn 容錯移轉叢集執行個體是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn 產品的一部分，會利用 Windows Server 容錯移轉叢集 (WSFC) 功能，透過伺服器執行個體層級 (「容錯移轉叢集執行個體 (FCI)」) 的備援提供本機高可用性。 FCI 是跨 Windows Server 容錯移轉叢集 (WSFC) 節點且可能跨多個子網路安裝的單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 在網路上，FCI 看似單一電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，但是 FCI 提供容錯移轉，可以在目前的 WSFC 節點無法使用時，從該節點容錯移轉到另一個節點。    
    
 如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)執行個體的容錯移轉叢集執行個體。    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 所導入的企業級高可用性災害復原方案，讓您可將一或多個使用者資料庫的可用性最大化。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須位於 Windows Server 容錯移轉叢集 (WSFC) 節點上。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)。    
    
  
>  **注意！** FCI 可以利用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 提供資料庫層級的遠端災害復原。 如需詳細資訊，請參閱[容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)。    
    
*  資料庫鏡像。 **注意！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我們建議您改用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 。     
資料庫鏡像是支援近乎瞬間的容錯移轉，進而提高資料庫可用性的方案。 資料庫鏡像可用以維護實際執行的資料庫 (稱為 *「主體資料庫」*) 所對應的單一待命資料庫 (或稱 *「鏡像資料庫」*)。 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。    
    
*  記錄傳送    
 記錄傳送就像 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 與資料庫鏡像一樣，都是在資料庫層級運作。 您可以使用記錄傳送來針對單一實際執行資料庫 (稱為「主要資料庫」) 維護一個或多個暖待命資料庫 (稱為「次要資料庫」)。 如需記錄傳送作業的相關資訊，請參閱[關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)。    
    
##  <a name="RecommendedSolutions"></a> 使用 SQL Server 保護資料的建議方案    
 為您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境提供資料保護的建議：    
    
-   對於透過協力廠商共用磁碟方案 (SAN) 的資料保護，我們建議您使用 AlwaysOn 容錯移轉叢集執行個體。    
    
-   對於透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料保護，我們建議您使用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。    
    
       >  如果您執行不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]版本，建議使用記錄傳送。 如需支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]版本的相關資訊，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)的＜高可用性 (AlwaysOn)＞一節。    
    
## <a name="see-also"></a>另請參閱    
 [SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [資料庫鏡像：互通性與共存性 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [SQL Server 2016 中已被取代的 Database Engine 功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  

