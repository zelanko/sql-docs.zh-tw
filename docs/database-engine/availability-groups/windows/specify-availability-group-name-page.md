---
title: "指定可用性群組選項頁面 (新增可用性群組精靈/新增資料庫精靈) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c12b2607c1f1ecd50d61e2b73646b040a2bbc338
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="specify-availability-group-options-page"></a>指定可用性群組選項頁面
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述 [指定可用性群組名稱] 頁面的選項。 本主題同時適用於 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 的 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 和 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
##  <a name="PageOptions"></a> 指定可用性群組選項  
 **可用性群組名稱**  
 指定可用性群組的名稱。 若為新的可用性群組，請指定在 Windows Server 容錯移轉叢集 (WSFC) 之所有可用性群組中唯一的有效 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別碼。 可用性群組名稱的最大長度為 128 個字元。  

 **叢集類型**：接下來，指定叢集類型。 可能的叢集類型取決於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本和作業系統。 從下列清單中，選擇其中一個：

   * **Windows Server 容錯移轉叢集**
   
      使用時機是將可用性群組裝載於屬於可進行高可用性和災害復原之 Windows Server 容錯移轉叢集的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時。 適用於所有支援的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本。 

   * **EXTERNAL**
      
      使用時機是將可用性群組裝載於外部叢集技術 (例如 Linux 上的 Pacemaker) 針對高可用性和災害復原所管理的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時。 適用於 [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 和更新版本。

   * **NONE**
      
      使用時機是將可用性群組裝載於叢集技術未針對讀取規模和負載平衡所管理的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體時。 適用於 [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 和更新版本。 
 
   **資料庫層級健全狀況偵測：**核取此方塊，以啟用可用性群組的資料庫層級健全狀況偵測 (DB_FAILOVER) 選項。 資料庫健全狀況偵測注意到資料庫不再處於線上狀態、發生錯誤，以及觸發可用性群組的自動容錯移轉。 請參閱 [SQL Server AlwaysOn 資料庫健全狀況偵測容錯移轉選項](sql-server-always-on-database-health-detection-failover-option.md)。


選取資料庫頁面 (新增可用性群組精靈和加入資料庫精靈)  
  
##  <a name="LaunchWiz"></a> 相關工作  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用將資料庫加入至可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
